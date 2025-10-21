# Hacknet 主题文件使用指南

## 概述

Hacknet 主题文件是用于自定义游戏主题的 XML 配置文件

## 文件结构

### 基本结构

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CustomTheme>
  <!-- 配置项 -->
</CustomTheme>
```

## 主要配置项

### 1. 主题布局 (`themeLayoutName`)

定义窗口的基本布局样式，可选值（这里指的是原版Hacknet的主题的布局）：

- `blue` - 蓝色主题
- `green` - 绿色主题
- `white` - 白色主题
- `mint` - 薄荷主题
- `greencompact` - 紧凑绿色主题
- `riptide` - 激流主题
- `colamaeleon` - 变色龙主题
- `riptide2` - 激流2主题

### 2. 背景图片 (`backgroundImagePath`)
在标签里输入你的背景图片的相对路径


### 3. 核心颜色配置

#### 主要颜色

- `defaultHighlightColor` - 网络地图节点颜色
- `defaultTopBarColor` - 顶部系统栏颜色
- `moduleColorSolidDefault` - 模块窗口边框颜色
- `moduleColorStrong` - 模块填充颜色
- `moduleColorBacking` - 全屏背景色

#### 执行程序模块

- `exeModuleTopBar` - EXE顶部栏颜色
- `exeModuleTitleText` - EXE标题文本颜色

### 4. 界面元素颜色

#### 功能按钮

- `warningColor` - 警告/可视化界面按钮颜色
- `subtleTextColor` - 次要文本颜色
- `darkBackgroundColor` - 搜索框/邮件按钮背景色

#### 背景和边框

- `indentBackgroundColor` - 登录模块背景色
- `outlineColor` - 节点连接线颜色

#### 端口状态

- `lockedColor` - 端口锁定/取消按钮颜色
- `brightLockedColor` - 端口不可破解背景色
- `unlockedColor` - 端口解锁后颜色
- `brightUnlockedColor` - 成功状态颜色

### 5. 文本和界面

- `terminalTextColor` - 终端文本颜色
- `topBarTextColor` - 顶部栏文本颜色
- `netmapToolTipColor` - 网络地图提示文字颜色
- `netmapToolTipBackground` - 网络地图提示背景色

### 6. 特殊效果

- `scanlinesColor` - 扫描线效果颜色
- `thisComputerNode` - 玩家计算机节点颜色
- `connectedNodeHighlight` - 当前连接节点高亮色




## 使用示例
标准的Theme文件见[Chronomia.xml](./../Assets/Themes/Chronomia.xml)



### 示例主题文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<CustomTheme>
  <themeLayoutName>blue</themeLayoutName>
  <backgroundImagePath>Themes/Backgrounds/your_image.png</backgroundImagePath>
  
  <defaultHighlightColor>255,41,63</defaultHighlightColor>
  <defaultTopBarColor>74,7,14,255</defaultTopBarColor>
  <moduleColorSolidDefault>0,204,132</moduleColorSolidDefault>
  
  <!-- 更多颜色配置 -->
</CustomTheme>
```



## 标准示例文件

- 查看 [Chronomia.xml](./../Assets/Themes/Chronomia.xml) 获取标准配置
- 参考游戏示例主题文件学习最佳实践


