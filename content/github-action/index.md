---
emoji: 🔁
title: Github Action을 활용한 자동 배포
date: '2022-05-20 17:00:00'
author: Ubi
tags: DevOps CI/CD
categories: DevOps
---

인사팀에서 데이터지원팀으로 이동하여 `BI (Buisiness Intelligence) 시스템` 작업을 약 세 달간 작업을 했고 내부 런칭까지 잘 마쳤다.  

기술적으로 부족한 부분도 매우 많고 앞으로 개선해야 할 부분들도 매우 많은 것을 다시 한번 느꼈다.  

하나 둘씩 기존의 방식을 개선하기 위해 최근에 여러 인프라 적인 요소, 개발 패러다임, 아키텍처 등을 도입하려 하고 있는데 혼자 하려니 쉽지 않았다.  

관련 회고는 다음에 조금 더 깊게 글로 남겨 내가 부족했던 점, 환경의 한계, 변명등을 남겨봐야겠다.  

오늘은 그에 앞서 Github Action을 활용하여 서비스의 배포 프로세스를 정리한 내용을 리뷰해보려고 한다.

그동안 sh을 이용하여 각자 개발자들의 시스템에서 배포하던 말도 안되는 프로세스로 이루어지고 있었다.  
나 또한 인사팀의 1인 개발자로 있을 때 그저 `yarn run deploy`로 배포를 하곤 했었는데, 당연히 잘못된건지 알면서도 코드를 수정하는 주체가 나 혼자 밖에 없었고 굳이 CI/CD까지 구축해야하나? 라는 생각이 머리 한 편에 자리잡고 있었다.  

그 상태로 팀에서 개발자가 조금 충원되고 CI/CD나 git 정책들을 미리 정리하여 관리하려고 했지만 일이 많다는 핑계로 당연하게도 미뤄졌고 결국 해당 부분을 제대로 마무리 짓지 못한 채 팀을 옮기게 되었다. (미안해요 전팀분들..)  

---

현재 개발한 BI 시스템의 프론트엔드는 `yarn` `vite` `vue3` 등의 스택으로 이루어져 있고, 백엔드는 `flask` 를 이용해 구축되어 있다.  

아직 `docker`를 활용한 이미지화 시킨 배포와 `blue/green` 배포까지는 적용하지 못했지만 차근차근 시간이 날 때마다 하나씩 적용시켜 나갈 계획이지만, 현재는 `ssh`로 `rsync`를 통해 배포를 진행하고 있는 열악한 상황이다.  

백엔드는 `uwsgi`로 돌고 있고 flask의 파이썬 코드들만 올라가면 되어 특별한 점이 없고, 프론트엔드가 그나마 빌드 등 몇가지 작업들을 거치는 workflow로 이루어 져 있기 때문에 여기서 작업한 내용을 간단하게 정리해본다.

---

`(다짜고짜 yml 투척)`  

```yaml
name: Dev Deployment

on:
  push:
    branches:
      - dev

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout source code
        uses: actions/checkout@master

      # setup yarn & node
      - name: Set up Node.js
        uses: actions/setup-node@master
        with:
          node-version: 16

      - name: Get yarn cache directory path
        id: yarn-cache-dir-path
        run: echo "::set-output name=dir::$(yarn cache dir)"

      - uses: actions/cache@v3
        id: yarn-cache
        with:
          path: ${{ steps.yarn-cache-dir-path.outputs.dir }}
          key: ${{ runner.os }}-yarn-${{ hashFiles('**/yarn.lock') }}
          restore-keys: |
            ${{ runner.os }}-yarn-
      - name: Install Yarn
        # if: steps.yarn-cache.outputs.cache-hit != 'true'
        run: yarn install --prefer-offline

      - name: Build Package
        run: yarn run prestg:deploy

      - name: Get Current Github action IP
        id: ip
        uses: haythem/public-ip@v1.2

      - name: Setting environment variables..
        run: |
          echo "AWS_DEFAULT_REGION=ap-northeast-2" >> $GITHUB_ENV
          echo "AWS_SG_NAME=default" >> $GITHUB_ENV
      - name: Add Github Actions IP to Security group
        run: |
          aws ec2 authorize-security-group-ingress --group-id ${{ secrets.AWS_SG_ID }} --protocol tcp --port 22 --cidr ${{ steps.ip.outputs.ipv4 }}/32
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: ${{ env.AWS_DEFAULT_REGION }}

      - name: Run SSH to Deploy
        run: |
          echo "$PRIVATE_KEY" > private_key && chmod 600 private_key
          rsync -avz --delete -e "ssh -o StrictHostKeyChecking=no -i private_key" ./dist ${USER_NAME}@${HOST_NAME}:/srv
        env:
          PRIVATE_KEY: ${{ secrets.AWS_PRIVATE_KEY  }}
          HOST_NAME: ${{ secrets.HOST_NAME  }}
          USER_NAME: ${{ secrets.USER_NAME  }}

      - name: Remove Github Actions IP from security group
        run: |
          aws ec2 revoke-security-group-ingress --group-id ${{ secrets.AWS_SG_ID }} --protocol tcp --port 22 --cidr ${{ steps.ip.outputs.ipv4 }}/32
        env:
          AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
          AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
          AWS_DEFAULT_REGION: ${{ env.AWS_DEFAULT_REGION }}
        if: always()
```

