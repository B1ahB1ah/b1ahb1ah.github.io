---
title: 0x04_hexo categories和tags页面不显示解决方法
date: 2019-2-20 02:55:06
categories: hexo博客
tags: 
	- hexo
	- categories
	- tags
---

#### BUG的发现

添加B1og的`categories`和`tags`模块时：

```
hexo new page "tags"
hexo new page "categories"
```

发现显示空白

<br />

<!-- more -->

#### 解决方法

1. 编辑`/source/tags/index.md`，添加如下代码：

   ```
   layout: "tags"
   ```

2. 编辑/source/categories/index.md，添加如下代码：

   ``` 
   layout: "categories"
   ```

   

