---
layout: post
title: Build Your Github Blog Without Themes
categories: General
---

# 拒绝模版！用Github搭博客的简易指南

### 准备 Github Page 与 Jekyll

#### 1 准备好一个Github Page仓库

在Github新建名为`*your_user_name*.github.io`的仓库。

#### 2 准备好Jekyll

根据Jekyll的[官方文档](https://jekyllrb.com/docs/)中的Quickstart一栏在本地安装好Jekyll，使得在自己的项目文件夹下执行`jekyll serve`后能在浏览器中访问`http://localhost:4000`并看到一个模版页面。如果这个过程报错了，很可能是缺少webrick（虽然以后不会用到的）。可以在项目文件夹中尝试如下两个命令后再`jekyll serve`：

```bash
bundle add webrick
gem install webrick
```

### 开始搭建基本结构

#### 0 从零开始

删除刚刚创建的模版网页的项目文件夹。将自己的Github Page仓库克隆下来。

```bash
git clone *your_user_name*.github.io
```

进入克隆的空文件夹。

#### 1 创建主页

首先在自己的项目文件夹按如下结构新建文件与文件夹：

```
username.github.io/
	index.md
	_config.yml
	_layouts/
		default.html
	
```

#### 2 _config.yml

这个文件是用来配置jekyll的文件，当网站内容逐渐丰富后需要更多配置，现在可以暂时写入如下内容：

```yaml
name: NAME OF YOUR BLOG
markdown: kramdown
```

其中，kramdown是jekyll所用的markdown生成器。

#### 3 index.md

这个文件将是你的博客的主页！试着写入以下内容：

```markdown
# Welcome
Hello Elwin!
```

#### 4 _layouts/default.html

这个`default.html`将是每个页面的默认框架，类似于网页内容的“壳”。我们用mardown写的博客都会被套上这个“壳”显示出来。

```html
<!DOCTYPE html>
<html>
	<head>
		<title>{% raw %}{{ page.title }}{% endraw %}</title> <!-- 显示套这个壳的markdown页面的标题 -->
	</head>
	<body>
        
		<nav> <!-- 导航区 -->
			<ul>
				<h1>HelloElwin's Blog</h1> <!-- 你的博客名字 -->
				<li><a href="/">Home</a></li>
				<li><a href="/all">All Posts</a></li>
			</ul>
		</nav>
        
		<div class="container">
			{% raw %}{{ content }}{% endraw %} <!-- 调用这个壳的markdown中的内容 -->
		</div>
		
		<footer> <!-- 页脚 -->
			<ul>
				<p>Designed by HelloElwin (2022)</p> 
			</ul>
		</footer>
        
	</body>
</html>
```

#### 5 启动！

此时运行`jekyll serve`，进入localhost即可看到网站的雏形！很丑对吧。但没关系，可以晚一些再开始写css。

#### 6 上传！

记得将仓库同步到github，这样就通过`*your_user_name.github.io`访问自己的网站了（可能有几分钟的延迟）。

```bash
git add .
git commit -m 'created main page'
git push
```

### 更进一步

#### 1 写一篇博客

在项目文件夹下新建如下文件和文件夹：

```
username.github.io/
	...(之前的东西)...
	_posts/
		2022-01-01-my-first-post.md
```

于是便有了一篇博客。注意！这个文件名格式必须是`YYYY-MM-DD-NAME.md`。同时，文件中应包含如下内容：

```markdown
---
layout: default
title: My First Post
---
# Welcome!
This is my first post!
```

可见在这里，我们请求套上了`_layouts/default.html`的壳，并声明了文章的名字。回头看看`default.html`，此处`title: My First Post`声明的名字就是被`{% raw %}{{ page.title }}{% endraw %}`调用了，同时后面的内容就对应了`{% raw %}{{ content }}{% endraw %}`。

#### 2 怎么阅读它？

你可能发现了之前博客主页上的`All Posts`点进去啥也没有。现在，请新建这些文件与文件夹：

```
username.github.io/
	...(之前的东西)...
	all/
		index.html
```

同时，在这个`index.html`中写入如下内容：

```html
---
layout: default
title: All Post
---

<h1> All Posts </h1>

<div>
	<ul class="post-list">
        
	{% raw %}{% for post in site.posts %}{% endraw %}
		<li>
			<span class="date">{% raw %}{{ post.date | date_to_string }}{% endraw %}</span>
			<a href="{{ post.url }}" title="{{ post.title }}">
				{% raw %}{{ page.title }}{% endraw %}
			</a>
		</li>
	{% raw %}{% endfor %}{% endraw %}

	</ul>
</div>
```

这样，它就会用for循环把所有博文罗列出来！

#### 3 试一试

现在再去localhost试试，这样就可以点进`All Posts`并看到自己的博文啦！没问题的话记得可以`git push`噢！

### 再进一步

接下来就可以试着写一写css（在项目文件夹新建`css/main.css`），以及去详细阅读Jekyll的[官方文档](https://jekyllrb.com/docs/)，尝试为博客加入更多细节了。祝好运！
