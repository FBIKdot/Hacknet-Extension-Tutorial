# Get Start

首先, 要制作一个Hacknet扩展, 你需要准备的内容大致如下:

- Hacknet 最新版本
- 一台可以正常玩Hacknet的电脑
- 一个可以正常使用的文本编辑器 ([VSCode](https://code.visualstudio.com/), [nvim](https://neovim.io/) ...等等)
- `xml`相关语法知识

# 工作环境准备

Hacknet扩展的大量内容通过`xml`(可扩展标记语言) 文件记录. 这是个**非常简单**的语言, 这里不做过多介绍. 

推荐使用[`Visual Studo Code`](https://code.visualstudio.com/)对扩展进行编辑, 因为[Hacknet-VSCode](https://github.com/AutumnRivers/hacknet-vscode)扩展可以实现hacknet扩展相关标签的自动补全. 如果你记不住标签可以使用它补全标签, 虽然并不特别智能. 

你需要安装最新版Hacknet来对扩展进行调试. 
Hacknet有**专门的调试模式**与**语法检测功能**, 它可以**极大的**提高扩展的调试效率. 
Hacknet的特性非常多, 你也许需要频繁的调试, 因此扩展的制作很难离开它. 

找到Hacknet的根目录, 在子目录`Extensions`下创建用于存放hacknet扩展的新目录. 这个目录将成为**扩展的根目录**, 也是接下来你的工作目录. 

如果你已经准备好了, 请前往 [Extension](./Content/Extension.md).