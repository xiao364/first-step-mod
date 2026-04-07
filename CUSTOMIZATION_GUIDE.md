# First Steps Mod - 标题自定义指南

## 概述

First Steps Mod 允许玩家通过修改语言文件（JSON）来自定义结构标题的显示效果，包括颜色、样式、显示时长等。

## 文件位置

语言文件位于：
```
assets/firststeps/lang/
```

根据您的游戏语言选择对应的文件：
- `zh_cn.json` - 简体中文
- `zh_tw.json` - 繁体中文（台湾）
- `zh_hk.json` - 繁体中文（香港）
- `en_us.json` - 英语（美国）
- `de_de.json` - 德语
- `ru_ru.json` - 俄语
- ... 其他语言

## 可自定义选项

### 1. 结构标题颜色

为特定结构设置自定义颜色：

```json
"structure.minecraft.desert_pyramid.color": "FFAA00"
```

**格式说明：**
- 使用 6 位十六进制颜色代码（不带 # 前缀）
- 例如：`FFAA00` (橙色), `00AAFF` (蓝色), `FF0000` (红色)

**示例：**
```json
"structure.minecraft.desert_pyramid.color": "FFAA00",
"structure.minecraft.ancient_city.color": "AA00FF",
"structure.terralith.castle.color": "00FFAA"
```

### 2. 标题文本样式

为标题添加粗体、斜体、下划线或删除线：

```json
"structure.minecraft.desert_pyramid.bold": "true",
"structure.minecraft.desert_pyramid.italic": "true",
"structure.minecraft.desert_pyramid.underline": "true",
"structure.minecraft.desert_pyramid.strikethrough": "true"
```

**可用选项：**
- `.bold` - 粗体 (`true` 或 `false`)
- `.italic` - 斜体 (`true` 或 `false`)
- `.underline` - 下划线 (`true` 或 `false`)
- `.strikethrough` - 删除线 (`true` 或 `false`)

**注意：** 设置为 `"false"` 或不添加该键则禁用该样式。

### 3. 显示时长

自定义标题的淡入、停留和淡出时间（以 ticks 为单位，20 ticks = 1 秒）：

```json
"structure.minecraft.desert_pyramid.fadein": "10",
"structure.minecraft.desert_pyramid.stay": "70",
"structure.minecraft.desert_pyramid.fadeout": "20"
```

**默认值：**
- `fadein`: 10 (0.5 秒)
- `stay`: 70 (3.5 秒)
- `fadeout`: 20 (1 秒)

**示例 - 延长显示时间：**
```json
"structure.minecraft.desert_pyramid.fadein": "20",
"structure.minecraft.desert_pyramid.stay": "120",
"structure.minecraft.desert_pyramid.fadeout": "30"
```

### 4. 模组前缀颜色

自定义模组前缀的显示颜色：

```json
"firststeps.prefix.minecraft.color": "FFAA00",
"firststeps.prefix.terralith.color": "00AAAA",
"firststeps.prefix.qrafty.color": "AA00AA",
"firststeps.prefix.repurposed_structures.color": "AA5500"
```

### 5. 维度名称颜色

自定义维度副标题的颜色：

```json
"firststeps.overworld.color": "55FF55",
"firststeps.the_nether.color": "FF5555",
"firststeps.the_end.color": "AA00AA",
"firststeps.unknown_dimension.color": "AAAAAA"
```

## 完整示例

以下是一个完整的自定义配置示例（沙漠神殿）：

```json
{
  "_comment": "First Steps Mod - Custom Configuration Example",
  "_version": "0.85",
  
  "structure.minecraft.desert_pyramid": "沙漠神殿",
  "structure.minecraft.desert_pyramid.color": "FFAA00",
  "structure.minecraft.desert_pyramid.bold": "true",
  "structure.minecraft.desert_pyramid.italic": "false",
  "structure.minecraft.desert_pyramid.underline": "false",
  "structure.minecraft.desert_pyramid.strikethrough": "false",
  "structure.minecraft.desert_pyramid.fadein": "10",
  "structure.minecraft.desert_pyramid.stay": "70",
  "structure.minecraft.desert_pyramid.fadeout": "20",
  
  "firststeps.prefix.minecraft.color": "FFAA00",
  "firststeps.overworld.color": "55FF55"
}
```

## 添加自定义结构

如果某个模组结构没有翻译，您可以手动添加：

```json
"structure.custommod.custom_structure": "自定义结构名称",
"structure.custommod.custom_structure.color": "FF00FF",
"structure.custommod.custom_structure.bold": "true"
```

**格式：** `structure.<命名空间>.<结构路径>`

## 注意事项

1. **版本兼容性**：修改语言文件后，建议更新文件中的 `"_version"` 字段以便追踪
2. **JSON 格式**：确保 JSON 格式正确，键值对之间用逗号分隔
3. **游戏重启**：修改语言文件后需要重启游戏才能生效
4. **备份建议**：修改前备份原始语言文件

## 故障排除

### 标题不显示
- 检查 JSON 格式是否正确
- 确认结构命名空间和路径正确
- 查看游戏日志获取错误信息

### 颜色不生效
- 确保使用 6 位十六进制代码（不带 #）
- 检查是否有拼写错误

### 样式不生效
- 确保使用 `"true"` 或 `"false"`（字符串形式，不是布尔值）
- 检查键名拼写是否正确

## 技术支持

如有问题，请查看：
- 模组配置文件：`config/firststeps.json`
- 游戏日志：`logs/latest.log`
- 模组版本：当前版本 0.85
