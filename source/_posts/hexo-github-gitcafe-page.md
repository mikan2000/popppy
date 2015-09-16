title: hexo同时部署github和gitcafe
date: 2015-09-16 14:15:55
tags: hexo多部署,hexo部署
---
首先修改hexo blog根路径下的_config.yml

找到deploy，按如下方式修改

```sh
deploy:
- type: git
  repo: git@github.com:username/username.github.io.git
  branch: master
- type: git
  repo: git@gitcafe.com:username/username.git
  branch: gitcafe-pages
```

添加SSH公钥后执行
```sh
hexo deploy
```