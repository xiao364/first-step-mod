# First Steps 结构汉化与自定义指南

这篇指南介绍如何给结构添加中文名称，以及修改标题颜色、大小和音效。

---

## 目录

1. [结构兼容说明](#结构兼容说明)
2. [快速汉化结构](#快速汉化结构)
3. [查找结构 ID](#查找结构-id)
4. [手动添加结构](#手动添加结构)
5. [自定义标题样式](#自定义标题样式)
6. [常见问题](#常见问题)

---

## 结构兼容说明

First Steps 会自动读取已安装模组中的结构。大部分结构不需要手动适配，就能出现在结构列表中并正常显示初见标题。

少数模组使用了特殊的建筑生成方式，可能仍会出现检测不到的情况。这类结构需要单独适配。

简单判断方法：

- 能显示标题，但名称是英文：添加中文翻译即可。
- 没出现在配置列表：可以手动添加结构 ID。
- 进入结构后完全没有反应：手动添加和翻译都无法修复，需要进一步排查。

---

## 快速汉化结构

假设结构 ID 是：

```text
trek:overworld/very_common/plains
```

在资源包中创建：

```text
你的资源包/
├── pack.mcmeta
└── assets/
    └── firststeps/
        └── lang/
            └── zh_cn.json
```

在 `zh_cn.json` 中写入：

```json
{
  "structure.trek.overworld.very_common.plains": "平原遗迹"
}
```

启用资源包并重新加载资源后，该结构就会显示为“平原遗迹”。

### 翻译键写法

格式：

```text
structure.<模组ID>.<结构路径>
```

如果结构路径包含 `/`，需要在翻译键中改成 `.`。

| 结构 ID | 翻译键 |
|---------|--------|
| `minecraft:desert_pyramid` | `structure.minecraft.desert_pyramid` |
| `terralith:volcano` | `structure.terralith.volcano` |
| `trek:overworld/very_common/plains` | `structure.trek.overworld.very_common.plains` |

多个结构可以写在同一个文件中：

```json
{
  "structure.minecraft.desert_pyramid": "沙漠神殿",
  "structure.terralith.volcano": "火山",
  "structure.trek.overworld.very_common.plains": "平原遗迹"
}
```

---

## 查找结构 ID

可以通过以下方式查找：

1. 进入世界后，打开 First Steps 的结构列表。
2. 输入 `/locate structure`，使用 Tab 补全。
3. 开启 First Steps 调试日志，查看实际检测到的结构 ID。

结构 ID 通常是：

```text
模组ID:结构名称
```

例如：

```text
minecraft:ancient_city
terralith:volcano
```

如果翻译没有生效，请先确认实际结构 ID，不要根据建筑名称猜测。

---

## 手动添加结构

手动添加可以让结构出现在 First Steps 配置列表中，方便设置名称和样式。

### 配置界面添加

打开 First Steps 配置页，在结构列表的添加框中输入完整结构 ID：

```text
terralith:underground/dungeon
```

### 配置文件添加

关闭游戏后，打开：

```text
config/firststeps.json
```

把结构加入已有的 `addedStructures`：

```json
{
  "addedStructures": [
    "terralith:underground/dungeon",
    "trek:overworld/very_common/plains"
  ]
}
```

不要使用上面的片段覆盖整个配置文件。

> 手动添加只会把结构加入配置列表，不能修复结构检测问题。

---

## 自定义标题样式

样式可以和翻译写在同一个 Lang 文件中。

### 常用设置

| 设置 | 示例 | 说明 |
|------|------|------|
| `color` | `FFAA00` | 标题颜色，不要添加 `#` |
| `bold` | `true` | 粗体 |
| `italic` | `true` | 斜体 |
| `shadow` | `false` | 是否显示阴影 |
| `opacity` | `80` | 不透明度，范围 0-100 |
| `scale` | `120` | 大小，100 为默认大小 |
| `stay` | `80` | 停留时间，20 约等于 1 秒 |
| `sound` | `minecraft:block.note_block.pling` | 进入结构时播放的音效 |
| `volume` | `50` | 音量，范围 0-100 |

### 示例

```json
{
  "structure.minecraft.desert_pyramid": "沙漠神殿",
  "structure.minecraft.desert_pyramid.color": "FFAA00",
  "structure.minecraft.desert_pyramid.bold": "true",
  "structure.minecraft.desert_pyramid.scale": "120",
  "structure.minecraft.desert_pyramid.stay": "80",
  "structure.minecraft.desert_pyramid.sound": "minecraft:block.note_block.pling",
  "structure.minecraft.desert_pyramid.volume": "50"
}
```

### 分别设置主标题和副标题

```json
{
  "structure.minecraft.ancient_city": "远古城市",
  "structure.minecraft.ancient_city.title.color": "FF5555",
  "structure.minecraft.ancient_city.title.bold": "true",
  "structure.minecraft.ancient_city.subtitle.color": "AAAAAA"
}
```

### 禁用某个结构

```json
{
  "structure.minecraft.mineshaft.show": "false"
}
```

### 禁用某个结构的音效

```json
{
  "structure.minecraft.stronghold.sound": "",
  "structure.minecraft.stronghold.volume": "0"
}
```

---

## 常见问题

### 中文名称没有生效

- 确认文件路径是 `assets/firststeps/lang/zh_cn.json`。
- 确认当前游戏语言是简体中文。
- 确认结构 ID 和翻译键完全对应。
- 路径中的 `/` 要改成 `.`。
- 重新加载资源包。

### 结构没有出现在列表中

先进入一个世界，再打开配置页。如果仍未出现，可以手动添加完整结构 ID。

### 进入结构后没有标题

- 确认 First Steps 已启用。
- 确认没有处于旁观者模式。
- 确认该结构没有被禁用。
- 开启调试日志，检查是否检测到结构 ID。

如果日志中始终没有该结构，添加翻译或手动加入列表都无法解决，需要提供结构 ID、模组版本和日志进行排查。

### JSON 文件无法加载

- 使用英文双引号。
- 最后一项后面不要加逗号。
- 文件使用 UTF-8 编码且不要带 BOM。
- Lang 文件应放在资源包中，不是数据包中。

---

最后更新：2026-07-11
