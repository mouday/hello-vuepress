# VuePress使用示例

[[toc]]

# 第一步 安装VitePress

VuePress是一个基于Vue驱动的静态网站生成器

安装

```bash
pnpm i vuepress
```

目录结构
```bash
$ tree -I node_modules -a
.
├── .github
│   └── workflows
│       └── vuepress-deploy.yml     # 自动部署到github
├── README.md
├── docs                            # 博客目录
│   ├── .vuepress        
│   │   └── config.js               # 配置文件
│   └── README.md                   # 博客首页 
├── package.json
└── pnpm-lock.yaml
```

站点配置config.js

```js
module.exports = {
  title: "VuePress 示例",
  description: "这是一个使用VuePress搭建的示例站点",
};

```
启动

```bash
# 安装依赖
pnpm i

# 运行开发环境
npm run dev

# 运行打包
npm run build
```

# 第二步 书写博客

使用markdown语法书写博客文章

# 第二步 部署到github

自动部署 vuepress-deploy.yml

```yaml
# doc https://github.com/jenkey2011/vuepress-deploy/

name: Build and Deploy
on: [push]

permissions:
  pull-requests: write
  issues: write
  repository-projects: write

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@master

    - name: vuepress-deploy
      uses: jenkey2011/vuepress-deploy@master
      env:
        ACCESS_TOKEN: ${{ secrets.GH_TOKEN }}
        TARGET_REPO: ${{ env.GITHUB_REPOSITORY }}
        TARGET_BRANCH: dist
        BUILD_SCRIPT: pnpm i && pnpm build
        BUILD_DIR: docs/.vuepress/dist
```

https://github.com/jenkey2011/vuepress-deploy/
