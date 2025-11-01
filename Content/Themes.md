# Themes（主题）

在Hacknet中，Themes用于给玩家使用的主题

一个Themes文件的结构如下:
```xml
<?xml version="1.0" encoding="UTF-8"?>
<CustomTheme>
  <!-- 窗口样式 -->
  <themeLayoutName>blue</themeLayoutName>

  <!-- This is a path to the background image file. It should be 1920x1080, and a .jpg or .png file.
  If this is left out, the theme will automatically generate a dynamic background for the theme-->
  <backgroundImagePath>Themes/Backgrounds/XXX.png</backgroundImagePath>
  
  <!-- Main Colors - these will define the main feel of the theme -->
  <!-- Color of nodes on the netmap, and many other derived colors. -->
  <!-- 管理员身份提示色 -->
  <defaultHighlightColor>230,235,50</defaultHighlightColor>
  <!-- 顶部系统栏 -->
  <defaultTopBarColor>40,88,160,125</defaultTopBarColor>
  <!-- This is used for the outlines of the module windows -->
  <!-- 模块描边 -->
  <moduleColorSolidDefault>110,240,230</moduleColorSolidDefault>
  <!-- 模块填充 -->
  <moduleColorStrong>0,0,0,120</moduleColorStrong>
  <!-- 全屏背景色 -->
  <moduleColorBacking>0,0,0,120</moduleColorBacking>

  <!-- EXE顶部栏 -->
  <exeModuleTopBar>0,128,255,150</exeModuleTopBar>
  <!-- EXE标题文本 -->
  <exeModuleTitleText>200,200,200,255</exeModuleTitleText>

  <!-- Extra Options -->
  <!-- 可视化界面按钮颜色 -->
  <warningColor>165,50,205</warningColor>
  <!-- 可视化界面登录按钮颜色 -->
  <subtleTextColor>150,30,180</subtleTextColor>
  <!-- 搜索框背景/邮件按钮等颜色 -->
  <darkBackgroundColor>8,8,8</darkBackgroundColor>
  <!-- use ram / 登录 模块背景色 -->
  <indentBackgroundColor>12,12,12</indentBackgroundColor>
  <!-- 节点之间连接线的颜色 -->
  <outlineColor>68,68,68</outlineColor>
  <!-- 断开/取消 按钮颜色、端口被锁住的颜色 -->
  <lockedColor>65,16,16,200</lockedColor>
  <!-- 显示端口不可破解的背景色 -->
  <brightLockedColor>160,0,0</brightLockedColor>
  <!-- sshcrack.exe小方格过度颜色、成功登录后成功两个字颜色等 -->
  <brightUnlockedColor>0,160,0</brightUnlockedColor>
  <!-- 端口解锁后的颜色 -->
  <unlockedColor>39,65,36</unlockedColor>
  <!-- MessageBoard使用 -->
  <lightGray>180,180,180</lightGray>
  <!-- 过载节点颜色[指RAM上的] 运行Shell时节点的颜色，以及您在[probe或nmap]看到的[检测到代理]和[检测到防火墙]的颜色 -->
  <shellColor>222,201,24</shellColor>
  <!-- shell过载按钮侧边颜色(经测试，按钮不够宽显示不出来侧边) -->
  <shellButtonColor>105,167,188</shellButtonColor>
  <!-- 模块bar文字色 -->
  <semiTransText>120,120,120,0</semiTransText>
  <!-- 终端文本颜色 -->
  <terminalTextColor>213,245,255</terminalTextColor>
  <!-- 顶部系统栏文本颜色 -->
  <topBarTextColor>255,255,255,150</topBarTextColor>
  <!-- 破解端口界面斜条纹颜色 -->
  <superLightWhite>2,2,2,30</superLightWhite>
  <!-- 当前连接的节点颜色 -->
  <connectedNodeHighlight>222,0,0,195</connectedNodeHighlight>
  <!-- 鼠标放到netmap节点上后显示右侧文字的颜色 -->
  <netmapToolTipColor>213,245,255,0</netmapToolTipColor>
  <!-- 鼠标放到netmap节点上后显示右侧文字的背景 -->
  <netmapToolTipBackground>0,0,0,70</netmapToolTipBackground>
  <!-- 顶部栏icon颜色 -->
  <topBarIconsColor>255,255,255</topBarIconsColor>
  <!-- 控制玩家计算机节点的颜色 -->
  <thisComputerNode>95,220,83</thisComputerNode>
  <!-- 搜索线的颜色 -->
  <scanlinesColor>255,255,255,15</scanlinesColor>
  
  <!-- AlienFX Colors used for Alienware (and other) hardware with variable LED lights that Hacknet can set dynamically -->
  <AFX_KeyboardMiddle>0,120,255</AFX_KeyboardMiddle>
  <AFX_KeyboardOuter>255,150,0</AFX_KeyboardOuter>
  <AFX_WordLogo>0,120,255</AFX_WordLogo>
  <AFX_Other>0,100,255</AFX_Other>
</CustomTheme>
```
一个Theme有以下几个部分:
- themeLayoutName 窗口样式（布局）
- backgroundImagePath 主题背景路径
- defaultHighlightColor 连接节点时Display窗口顶部显示的"您是本系统的管理员"
- defaultTopBarColor 顶部的系统栏显示的颜色
- moduleColorSolidDefault 每个模块的描边颜色
- moduleColorStrong 每个模块填充的颜色
- moduleColorBacking 全屏背景色
- exeModuleTopBar exe程序顶部栏的颜色
- exeModuleTitleText exe标题文本颜色
- warningColor 可视化界面颜色（Trace时闪的颜色）
- subtleTextColor 登录按钮的颜色
- darkBackgroundColor 搜索框背景/邮件按钮等颜色
- indentBackgroundColor 顶部内存条显示占用（USED ：RAM ??/??）的背景颜色
- outlineColor 节点之间的连接线颜色
- lockedColor 端口锁定状态的背景颜色（也是断开/取消的背景色）
- brightLockedColor 显示端口不可破解的背景色
- brightUnlockedColor ssh的小方格过渡颜色
- unlockedColor 端口开放背景色
- lightGray MessageBoard主题颜色
- shellColor 允许shell时节点的颜色
- shellButtonColor shell过载按钮左边框颜色
- semiTransText 模块bar文字色
- terminalTextColor 终端文本颜色
- topBarTextColor 顶部系统栏颜色
- superLightWhite 斜条纹颜色
- connectedNodeHighlight 当前连接的节点颜色
- netmapToolTipColor 把鼠标放在节点上显示的节点名颜色
- topBarIconsColor 顶部栏icon颜色
- thisComputerNode 本地计算机节点颜色
- scanlinesColor 搜索线的颜色
## 示例文件
可参考[Chronomia.xml](./../Assets/Themes/Chronomia.xml)

