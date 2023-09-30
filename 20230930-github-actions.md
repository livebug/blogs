---
title : 'Github Actions 使用 自动化发布博客' 
date : 2023-09-30T13:58:58+08:00
toc: true
---

介绍背景：

博客网站`myblog`仓库底下有两个子库，一个子库是用来存储`markdown`文章的`blogs`仓库，一个是用来存储`public`内容的`github pages`库 `livebug.github.io`仓库

当博客网站样式更新提交，或者文章提交，触发`myblog`仓库的 actions ，执行完之后发布到pages仓库


## 开发`myblog`仓库的提交 actions

```yaml
jobs:
  # Build job
  public:
    runs-on: ubuntu-latest
    env:
      HUGO_VERSION: 0.114.0
    steps:
      - name: Setup Hugo # 初始化 护工环境
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: "latest" 
      - name: Checkout # 检出资源
        uses: actions/checkout@v3
        with:
          submodules: recursive # 子模块，当前是 blogs 仓库
      - name: Build with Hugo   # 编译生成
        env:
          # For maximum backward compatibility with Hugo modules
          HUGO_ENVIRONMENT: production
          HUGO_ENV: production
        run: |
          hugo  
      - name: Deploy  # 发布
        uses: peaceiris/actions-gh-pages@v3
        with:
          personal_token: ${{ secrets.PERSONAL_TOKEN }} # 另外还支持 deploy_token 和 github_token
          external_repository: livebug/livebug.github.io # 修改为你的 GitHub Pages 仓库
          publish_dir: ./public
          publish_branch: master
```