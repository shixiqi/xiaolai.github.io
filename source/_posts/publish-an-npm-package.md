---
title: 如何在 npm 上发布一个包 (npm module/package)
date: 2016-05-23
tag: npm
---

在 nmpjs.com 上注册一个帐号；

{% codeblock %}
$ npm adduser
npm install -g pakmanager
{% endcodeblock %}

编辑好 `package.json` 之后，把项目 push 到 github 的 repo 里；而后在要发布的包文件夹里执行：

{% codeblock %}
$ cd /path/to/your-project
$ npm init
$ pakmanager deps
$ npm publish ./
{% endcodeblock %}

更新版本的方法是：

```bash
git checkout v1.0.7
npm publish ./

git checkout v1.1.3
npm tag foobar@1.1.3 latest
```

发布之后，去 npmjs.com 上检查核实一下，就好像这里：

https://www.npmjs.com/package/xpress-generator
