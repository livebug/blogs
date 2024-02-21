---
title : 'Hugo Actions Error'
date : 2024-02-21T13:16:55+08:00
toc: true
tags: ['hugo']
categories: ['技术博客']
---

My point was, you didn’t state that the problem was limited to building your site on GitHub pages. That would have been helpful.  
我的观点是，您没有说明问题仅限于在 GitHub 页面上构建您的网站。那本来会有所帮助。  
  
For anyone else stumbling across this post, this is completely unrelated to v0.108.0 vs. v0.109.0.  
对于偶然发现这篇文章的任何其他人，这与 v0.108.0 与 v0.109.0 完全无关。  
  
The problem was with the GitHub pages configuration file.  
问题出在 GitHub 页面配置文件上。  
  
Incorrect: 不對：  
```yaml
- name: Setup Hugo  
  uses: peaceiris/actions-hugo@v2  
  with:  
    hugo-version: 'latest'  
    # extended: true 
``` 
Correct: 正确：  
```yaml
- name: Setup Hugo  
  uses: peaceiris/actions-hugo@v2  
  with:  
    hugo-version: 'latest'  
    extended: true
```  
Here’s a clone of the repo with the correction:  
下面是带有更正的存储库的克隆：  
https://github.com/jmooring/hugo-forum-topic-42096 29  
  
And GitHib Pages builds the site as exected:  
GitHib Pages 按如下方式构建网站：  
https://jmooring.github.io/hugo-forum-topic-42096/ 17  


Because you are checking the resources directory into source control, Hugo doesn’t need the extended version if the cache is warm. But when the cache is cold, Hugo needs to transpile the SASS to CSS again, and it cannot do that without the extended version.  
因为你要把资源目录签入到源代码管理中，所以如果缓存是暖的，Hugo不需要扩展版本。但是当缓存很冷时，Hugo 需要再次将 SASS 转译为 CSS，如果没有扩展版本，它就无法做到这一点。

