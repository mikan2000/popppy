title: atom设置字体加粗
date: 2015-09-24 17:43:20
tags: atom
---
* 打开atom，按ctrl+shift+p，输入setting选择Settings View: Open

* 在左菜单中选择Settings这项，设置Font Family为inconsolata

* 点击左菜单的Open Config Folder，这时会打开一个新窗口

* 找到styles.less,添加如下代码

```less
.editor {
     font-weight: bold;
}
```