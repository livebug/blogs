---
title : 'hugo new content 命令使用 & 自定义新增文章脚本'
date : 2023-10-14T20:27:57+08:00
toc: true
# draft : true
tags :
- hugo
categories: ['技术博客']
---
hugo new content

创建新的内容文件并自动设置日期和标题。它将根据提供的路径猜测要创建的文件类型。

```bash
hugo new content [path] [flags]
```

hugo 新建文章，基本就是路径加文件名的命令，并不能只写名字，自动补全时间戳这种，自己写一个吧


```bash
# 基本新建命令
hugo new blogs/xxxxx.md
```
`hugonew.sh` 脚本
``` bash 
post_name=$1
post_name=`echo $post_name | tr -s ''` # 去除多余空格
post_name=` echo ${post_name} | sed 's/[ ]/-/g'` # 替换空格为 - 
echo ${post_name}
date_string=`date +%Y%m%d` # 日期字符串
date_string=`date +%Y%m%d%H%M%S` # 毫秒字符串
date
hugo new blogs/${post_name}.md $@
cd content/blogs/
mv ${post_name}.md ${date_string}-${post_name}.md
```
执行 自动拼接日期串 可以自己替换为毫秒字符串

```bash
sh hugonew.sh "tests    dsds SDASD    "
tests-dsds-SDASD
Sat Oct 14 22:19:43 CST 2023
Content "/home/sharif/myblog/content/blogs/tests-dsds-SDASD.md" created
```

小问题生成之后文件中，文章名中带了日期,修改脚本，先建立文件，然后替换文件名
