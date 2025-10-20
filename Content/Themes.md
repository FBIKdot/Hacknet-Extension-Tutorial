# Hacknet 主题文件使用指南

## 扩展信息

- **扩展名称**: YOU HACKER 2
- **语言**: 中文 (zh-cn)
- **起始主题**: HacknetBlue

## 概述

Hacknet 主题文件是用于自定义游戏界面的 XML 配置文件。通过修改主题文件，你可以完全改变游戏的外观和感觉。

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

设置自定义背景图片路径：

- 推荐分辨率：1920x1080
- 支持格式：JPG、PNG
- 路径相对于扩展目录

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

## 颜色格式

Hacknet 主题使用 RGBA 颜色格式：

- **RGB**: `红,绿,蓝` (每个值 0-255)
- **RGBA**: `红,绿,蓝,透明度` (透明度 0-255，0=完全透明，255=完全不透明)

## Chronomia 主题分析

### 主题特色

基于 Chronomia.xml 主题文件，它具有以下特点：

- **主色调**: 蓝色系 (30,111,233)
- **背景图片**: Themes/Backgrounds/Chronomia_jacket.png
- **终端文本**: 浅蓝色 (213,245,255)
- **模块边框**: 深蓝色 (53,59,238)
- **管理员提示**: 紫色 (4,0,255)

### 关键颜色配置

```xml
<!-- 管理员身份提示色 -->
<defaultHighlightColor>4,0,255</defaultHighlightColor>
<!-- 顶部系统栏 -->
<defaultTopBarColor>30,111,233</defaultTopBarColor>
<!-- 模块描边 -->
<moduleColorSolidDefault>53,59,238</moduleColorSolidDefault>
<!-- 终端文本颜色 -->
<terminalTextColor>213,245,255</terminalTextColor>
```

## 使用示例

### 创建新主题

1. 在 `Themes/` 目录下创建新的 XML 文件
2. 复制基本结构
3. 根据需要修改颜色值

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

## 安装方法

1. **将主题文件放入扩展目录**:

   - 将主题 XML 文件放入 `Themes/` 目录
   - 背景图片放入 `Themes/Backgrounds/` 目录
2. **在游戏中启用主题**:

   - 修改 `ExtensionInfo.xml` 中的 `<StartingTheme>` 标签
   - 或通过游戏内主题选择器切换
3. **重启游戏**应用新主题

   ```

   ```

## 最佳实践

### 1. 颜色搭配原则

- **保持一致性**: 确保颜色搭配协调
- **对比度**: 确保文本在背景上清晰可见
- **层次感**: 使用不同透明度创建视觉层次

### 2. 文件管理

- **备份原文件**: 修改前备份原始主题文件
- **渐进修改**: 每次只修改少量颜色进行测试
- **版本控制**: 为不同版本的主题创建备份

### 3. 测试建议

- **多环境测试**: 在不同光照条件下测试可读性
- **功能测试**: 确保所有界面元素都正常工作
- **性能测试**: 检查主题是否影响游戏性能

## 故障排除

### 常见问题

1. **主题不生效**: 检查文件路径和格式是否正确
2. **颜色显示异常**: 验证 RGBA 值是否在有效范围内
3. **背景图片不显示**: 确认图片路径和格式正确

### 调试技巧

- 使用示例主题作为基础模板
- 逐个修改颜色值进行测试
- 查看游戏日志文件获取错误信息

## 扩展资源

### 内置主题参考

- 查看 `Themes/ExampleTheme.xml` 获取标准配置
- 参考游戏原版主题文件学习最佳实践

### 工具推荐

- 使用颜色选择器工具获取精确的 RGB 值
- 使用图像编辑软件创建合适的背景图片

通过合理配置这些颜色值，你可以创建出符合个人喜好的独特 Hacknet 游戏界面。祝您创作愉快！
