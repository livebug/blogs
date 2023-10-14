---
title : 'Add Gitalk 评论组件'
date : 2023-10-14T22:51:48+08:00
toc: true
tags: ['hugo','gitalk']
categories: ['技术博客']
---

## 1. 增加模板页在主题的目录下 `themes/xxx/layouts/partials/gitalk.html`
```html
{{ if .Site.Params.enableGitalk }}
<div id="gitalk-container"></div>
<link rel="stylesheet" href="https://unpkg.com/gitalk/dist/gitalk.css">
<script src="https://unpkg.com/gitalk/dist/gitalk.min.js"></script>
<script>
  const gitalk = new Gitalk({
    clientID: '{{ .Site.Params.Gitalk.clientID }}',
    clientSecret: '{{ .Site.Params.Gitalk.clientSecret }}',
    repo: '{{ .Site.Params.Gitalk.repo }}',
    owner: '{{ .Site.Params.Gitalk.owner }}',
    admin: ['{{ .Site.Params.Gitalk.owner }}'],
    id: location.pathname, // Ensure uniqueness and length less than 50
    distractionFreeMode: false // Facebook-like distraction free mode
  });
  (function () {
    if (["localhost", "127.0.0.1"].indexOf(window.location.hostname) != -1) {
      document.getElementById('gitalk-container').innerHTML = 'Gitalk comments not available by default when the website is previewed locally.';
      return;
    }
    gitalk.render('gitalk-container');
  })();
</script>
{{ end }}
```
其中有一些参数

## 2.配置参数 `config.toml`

```toml
[params]
  enableGitalk = true
  [params.theme_config]
    appearance = "light"
    back_home_text = ".."
    date_format = "2006-01-02"
  [params.gitalk] 
    clientID = "QQQQQQQQQQQQQQQQ" # 您刚才创建Github Application 的 Client ID
    clientSecret = "QQQQQQQQQQQQQQQQ" # 您刚才创建Github Application 的 Client Secret
    repo = "livebug.github.io" # 您的博客的github地址Repository name，例如：xxxx.github.io
    owner = "livebug" # 您的GitHub ID
    admin= "livebug" # 您的GitHub ID
    id= "location.pathname" # 文章页面的链接地址就是ID
    labels= "gitalk" # Github issue labels. If you used to use Gitment, you can change it
    perPage= 15 # Pagination size, with maximum 100.
    pagerDirection= "last" # Comment sorting direction, available values are 'last' and 'first'.
    createIssueManually= true # 设置为true，如果是管理员登录，会自动创建issue，如果是false，需要管理员手动添加第一个评论(issue)
    distractionFreeMode= false # Enable hot key (cmd|ctrl + enter) submit comment.
```
其中有一些 `gitalk` 的基础信息，需要申请配置下

## 3. 申请`gitalk`信息
首先创建一个`OAuth application`应用，地址 https://github.com/settings/applications/new

![](/img/20201216163446137.png)
申请之后，选择`Generate a new client secret`
![](/img/2023-10-14-225937.png)

把 `clientID` 和 `clientSecret` 填到配置中

### 有个问题，这样直接填不就都暴露了嘛？？
https://github.com/gitalk/gitalk/issues/150#issuecomment-402366588

这里给了回答

>获取或修改 GitHub 用户数据，需要 token，为了拿到 token，除了需要 OAuth App 的 client_id 和 client_secret 外，还需要一个 Authorization Code。    
>这个 code 是 GitHub 登录授权完成时，在跳转回 redirect_uri 的查询参数拿到的， redirect_uri 必须是在 OAuth App 配置的 callback URL 域名下。  
>这样即使别人用了你的 client_id 和 client_secret ，跳转之后也拿不到 code，所以，有 client_id 和 client_secret 也做不了什么。