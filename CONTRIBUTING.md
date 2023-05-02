# Contributing Guidelines

欢迎来到这个项目! 感谢您的关注并欢迎您的贡献. 为确保每个人都能有效协作, 我们要求您在向此存储库贡献代码时遵循这些准则. 

## Git Commit Guidelines

请以以下格式进行commit:
~~~
更改类型: [文档标题]内容
~~~

项目的文档有关的标题可以只保留3个字母, 峰驼单词可以只取大写字母. 如`Nodes`为`[Nod]`, `HackerScript`为`[HS].

更改类型如下: 
- docs 对与项目的文档有关的修改
- - : 更改
- - +: 创建
- - -: 删除

- assets 对媒体的修改
- - : 更改
- - +: 创建
- - -: 删除

- repo 对仓库/项目定义的文本修改, 如`.gitignore`与`.github/ISSUE_TEMPLATE/xx.md`.
- - : 更改
- - +: 创建
- - -: 删除


## Example
假如提交对介绍`Action`的文档中的内容进行完善的改变, 则commit内容如下:
~~~
docs: [Act]完善了什么什么
~~~
假如创建了`.gitignore`, 内容为`.vscode/`, 则commit内容如下:
~~~
repo+: [gitignore]添加了.vscode
~~~
假如改变内容为对介绍`Nodes`的文档中的"守护进程"内容进行完善, 并且附加了部分媒体, 则应该分别提交. commit内容如下:
~~~
assets+: [Nod]添加了部分守护进程的图片
~~~
~~~
docs: [Nod]完善了守护进程
~~~

## Assets Guidelines
媒体内容应该按照以下标准来存放:

假如文档为:
~~~
目录/文件名.md
~~~
则它的媒体文件应该存放于:
~~~
Assets/目录/文件名/
~~~

在文中媒体内容应该使用相对路径引用, 这样方便于阅读器找到相应媒体.