---
emoji: ๐
title: Github Action์ ํ์ฉํ ์๋ ๋ฐฐํฌ (์์ฑ์ค)
date: '2022-05-20 17:00:00'
author: Ubi
tags: DevOps CI/CD
categories: DevOps
---

์ธ์ฌํ์์ ๋ฐ์ดํฐ์ง์ํ์ผ๋ก ์ด๋ํ์ฌ `BI (Buisiness Intelligence) ์์คํ` ์์์ ์ฝ ์ธ ๋ฌ๊ฐ ์์์ ํ๊ณ  ๋ด๋ถ ๋ฐ์นญ๊น์ง ์ ๋ง์ณค๋ค.  

๊ธฐ์ ์ ์ผ๋ก ๋ถ์กฑํ ๋ถ๋ถ๋ ๋งค์ฐ ๋ง๊ณ  ์์ผ๋ก ๊ฐ์ ํด์ผ ํ  ๋ถ๋ถ๋ค๋ ๋งค์ฐ ๋ง์ ๊ฒ์ ๋ค์ ํ๋ฒ ๋๊ผ๋ค.  

ํ๋ ๋์ฉ ๊ธฐ์กด์ ๋ฐฉ์์ ๊ฐ์ ํ๊ธฐ ์ํด ์ต๊ทผ์ ์ฌ๋ฌ ์ธํ๋ผ ์ ์ธ ์์, ๊ฐ๋ฐ ํจ๋ฌ๋ค์, ์ํคํ์ฒ ๋ฑ์ ๋์ํ๋ ค ํ๊ณ  ์๋๋ฐ ํผ์ ํ๋ ค๋ ์ฝ์ง ์์๋ค.  

๊ด๋ จ ํ๊ณ ๋ ๋ค์์ ์กฐ๊ธ ๋ ๊น๊ฒ ๊ธ๋ก ๋จ๊ฒจ ๋ด๊ฐ ๋ถ์กฑํ๋ ์ , ํ๊ฒฝ์ ํ๊ณ, ๋ณ๋ช๋ฑ์ ๋จ๊ฒจ๋ด์ผ๊ฒ ๋ค.  

์ค๋์ ๊ทธ์ ์์ Github Action์ ํ์ฉํ์ฌ ์๋น์ค์ ๋ฐฐํฌ ํ๋ก์ธ์ค๋ฅผ ์ ๋ฆฌํ ๋ด์ฉ์ ๋ฆฌ๋ทฐํด๋ณด๋ ค๊ณ  ํ๋ค.

๊ทธ๋์ sh์ ์ด์ฉํ์ฌ ๊ฐ์ ๊ฐ๋ฐ์๋ค์ ์์คํ์์ ๋ฐฐํฌํ๋ ๋ง๋ ์๋๋ ํ๋ก์ธ์ค๋ก ์ด๋ฃจ์ด์ง๊ณ  ์์๋ค.  
๋ ๋ํ ์ธ์ฌํ์ 1์ธ ๊ฐ๋ฐ์๋ก ์์ ๋ ๊ทธ์  `yarn run deploy`๋ก ๋ฐฐํฌ๋ฅผ ํ๊ณค ํ์๋๋ฐ, ๋น์ฐํ ์๋ชป๋๊ฑด์ง ์๋ฉด์๋ ์ฝ๋๋ฅผ ์์ ํ๋ ์ฃผ์ฒด๊ฐ ๋ ํผ์ ๋ฐ์ ์์๊ณ  ๊ตณ์ด CI/CD๊น์ง ๊ตฌ์ถํด์ผํ๋? ๋ผ๋ ์๊ฐ์ด ๋จธ๋ฆฌ ํ ํธ์ ์๋ฆฌ์ก๊ณ  ์์๋ค.  

๊ทธ ์ํ๋ก ํ์์ ๊ฐ๋ฐ์๊ฐ ์กฐ๊ธ ์ถฉ์๋๊ณ  CI/CD๋ git ์ ์ฑ๋ค์ ๋ฏธ๋ฆฌ ์ ๋ฆฌํ์ฌ ๊ด๋ฆฌํ๋ ค๊ณ  ํ์ง๋ง ์ผ์ด ๋ง๋ค๋ ํ๊ณ๋ก ๋น์ฐํ๊ฒ๋ ๋ฏธ๋ค์ก๊ณ  ๊ฒฐ๊ตญ ํด๋น ๋ถ๋ถ์ ์ ๋๋ก ๋ง๋ฌด๋ฆฌ ์ง์ง ๋ชปํ ์ฑ ํ์ ์ฎ๊ธฐ๊ฒ ๋์๋ค. (๋ฏธ์ํด์ ์ ํ๋ถ๋ค..)  

---

ํ์ฌ ๊ฐ๋ฐํ BI ์์คํ์ ํ๋ก ํธ์๋๋ `yarn` `vite` `vue3` ๋ฑ์ ์คํ์ผ๋ก ์ด๋ฃจ์ด์ ธ ์๊ณ , ๋ฐฑ์๋๋ `flask` ๋ฅผ ์ด์ฉํด ๊ตฌ์ถ๋์ด ์๋ค.  

์์ง `docker`๋ฅผ ํ์ฉํ ์ด๋ฏธ์งํ ์ํจ ๋ฐฐํฌ์ `blue/green` ๋ฐฐํฌ๊น์ง๋ ์ ์ฉํ์ง ๋ชปํ์ง๋ง ์ฐจ๊ทผ์ฐจ๊ทผ ์๊ฐ์ด ๋  ๋๋ง๋ค ํ๋์ฉ ์ ์ฉ์์ผ ๋๊ฐ ๊ณํ์ด์ง๋ง, ํ์ฌ๋ `ssh`๋ก `rsync`๋ฅผ ํตํด ๋ฐฐํฌ๋ฅผ ์งํํ๊ณ  ์๋ ์ด์ํ ์ํฉ์ด๋ค.  

๋ฐฑ์๋๋ `uwsgi`๋ก ๋๊ณ  ์๊ณ  flask์ ํ์ด์ฌ ์ฝ๋๋ค๋ง ์ฌ๋ผ๊ฐ๋ฉด ๋์ด ํน๋ณํ ์ ์ด ์๊ณ , ํ๋ก ํธ์๋๊ฐ ๊ทธ๋๋ง ๋น๋ ๋ฑ ๋ช๊ฐ์ง ์์๋ค์ ๊ฑฐ์น๋ workflow๋ก ์ด๋ฃจ์ด ์ ธ ์๊ธฐ ๋๋ฌธ์ ์ฌ๊ธฐ์ ์์ํ ๋ด์ฉ์ ๊ฐ๋จํ๊ฒ ์ ๋ฆฌํด๋ณธ๋ค.

---

`(๋ค์ง๊ณ ์ง yml ํฌ์ฒ)`  

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

ํ๋ํ๋์ฉ ์ดํด๋ณด๋๋ก ํ์

```yaml
name: Dev Deployment
```

`name`์ Github Actions์์ ์ฌ์ฉํ  ์ํฌํ๋ก์ฐ ์ด๋ฆ์ ๊ฐ๋ฆฌํค๊ณ  ์๋์ ๊ฐ์ด ์ข์ธก์ ํ์๋๋ค.
(์ด๋ฏธ์ง ์ฝ์)

```yaml
on:
  push:
    branches:
      - dev
```

`on`์ ์ด๋ ์ด๋ฒคํธ์ ํด๋น workflow๋ฅผ ํธ๋ฆฌ๊ฑฐ ํ  ์ง๋ฅผ ์ค์ ํด์ฃผ๋ ๋ถ๋ถ์ด๋ค. ์์ ๋ด์ฉ์ `dev` ๋ธ๋์น์ push hook์ด ๋ฐ์ํ์ ๋ ํด๋น workflow๋ฅผ ํธ๋ฆฌ๊ฑฐ ํ๊ฒ ๋ค๋ ์๋ฏธ์ด๋ค.  
(Github Action ์ค์ ์ ์งํํ๋ฉด์ ๋๊ผ์ง๋ง Jenkins์ ๋นํด ๋๋ฌด๋๋ฌด ์ง๊ด์ ์ด๊ณ  ์ฝ๊ฒ ๊ตฌ์ฑํ  ์ ์์๋ค.)  


`on`์์ ์ฌ์ฉํ  ์ ์๋ ์ด๋ฒคํธ๋ค์ [์ฌ๊ธฐ](https://docs.github.com/en/actions/using-workflows/events-that-trigger-workflows)์์ ์ฐธ๊ณ ํ  ๊ฒ.

> 