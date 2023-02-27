1. 创建github项目

![1677488601434](image/README/1677488601434.png)

2. 初始化本地仓库

```bash
git init
```

3. 重命名本地分支，以及设置远程分支

```bash
git remote add origin https://github.com/yuenci/react-gh-pages-action1.git
git branch -M main
git push -u origin main
```

4. Create gh-pages branch

Commit your project before your execute blow commands

```bash
git checkout -b gh-pages
# create a new branch
```

4. 获取token

前往 https://github.com/settings/tokens

![1677488794380](image/README/1677488794380.png)

![1677488821693](image/README/1677488821693.png)

5. 设置token

![1677488867294](image/README/1677488867294.png)![1677488903579](image/README/1677488903579.png)

6. 新建 [.github/workflows](https://github.com/yuenci/react-gh-pages-action/tree/master/.github/workflows "This path skips through empty directories") 文件夹，之后新建deploy.yml 文件

![1677489003136](image/README/1677489003136.png)

```yml
# deploy.yml
name: Build and Deploy
on:
  push:
    branches:
      - main # Set a branch to deploy

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout 🛎️
        uses: actions/checkout@v3

      - name: Install and Build 🔧 # This example project is built using npm and outputs the result to the 'build' folder. Replace with the commands required to build your project, or remove this step entirely if your site is pre-built.
        run: |
          npm install yarn -g
          yarn
          yarn build

      - name: Deploy 🚀
        uses: JamesIves/github-pages-deploy-action@v4
        with:
          folder: build # The folder the action should deploy.
          BRANCH: gh-pages # The branch the action should deploy to.
          Token: ${{ secrets.TOKEN }} # This token is provided by Actions, you do not need to create your own token.
```
