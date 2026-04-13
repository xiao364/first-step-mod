# First Steps 自定义标题指南

> 通过语言文件自定义每个结构的标题样式、显示行为和音效。
> 
> **支持版本：** 1.21 - 1.21.6+ | **Mod版本：** 0.98

---

## 目录

1. [快速开始](#快速开始)
2. [配置结构](#配置结构)
3. [所有配置项](#所有配置项)
   - [显示控制](#显示控制)
   - [显示时长](#显示时长tickst20-ticks--1秒)
   - [文本样式](#文本样式)
   - [渲染设置](#渲染设置)
   - [音效设置](#音效设置)
   - [标题与副标题分开设置](#标题与副标题分开设置)
   - [自定义颜色](#自定义颜色)
   - [全局样式Lang文件](#全局样式lang文件)
4. [完整示例](#完整示例)
5. [故障排除](#故障排除)
6. [服务器端样式同步](#服务器端样式同步)

---

## 快速开始

### 语言文件位置

在资源包或数据包中创建：
```
assets/firststeps/lang/<语言代码>.json
```

常用语言代码：
- `en_us.json` - 英文（美国）
- `zh_cn.json` - 简体中文
- `zh_tw.json` - 繁体中文

### 基础格式

```json
{
  "structure.<命名空间>.<结构名>.<属性>": "值"
}
```

### 示例 - 修改沙漠神殿样式

```json
{
  "structure.minecraft.desert_pyramid": "沙漠神殿",
  "structure.minecraft.desert_pyramid.color": "FFAA00",
  "structure.minecraft.desert_pyramid.bold": "true",
  "structure.minecraft.desert_pyramid.volume": "50"
}
```

---

## 配置结构

### 命名规则

| 结构类型 | 命名空间 | 结构名示例 |
|---------|---------|-----------|
| 原版结构 | `minecraft` | `desert_pyramid`, `jungle_pyramid`, `ancient_city` |
| 模组结构 | 模组ID | `terralith:volcano` → `terralith` + `volcano` |

### 获取结构ID

1. **游戏内查看**：进入结构后按 `F3`，查看屏幕右侧的 `SC` 行
2. **日志输出**：进入结构时模组会输出结构ID到日志（如开启调试）

---

## 所有配置项

### 显示控制

| 配置项 | 类型 | 默认值 | 说明 |
|-------|------|--------|------|
| `show` | 布尔 | `true` | 是否显示该结构的标题（完全禁用） |
| `showtitle` | 布尔 | `true` | 是否显示主标题 |
| `showsubtitle` | 布尔 | `true` | 是否显示副标题（维度信息） |

```json
{
  "structure.minecraft.desert_pyramid.show": "true",
  "structure.minecraft.desert_pyramid.showtitle": "true",
  "structure.minecraft.desert_pyramid.showsubtitle": "false"
}
```

### 显示时长（ticks，20 ticks = 1秒）

| 配置项 | 类型 | 默认值 | 有效范围 | 说明 |
|-------|------|--------|---------|------|
| `fadein` | 整数 | `10` | 0-6000 | 淡入时间 |
| `stay` | 整数 | `60` | 0-6000 | 保持显示时间 |
| `fadeout` | 整数 | `20` | 0-6000 | 淡出时间 |

```json
{
  "structure.minecraft.desert_pyramid.fadein": "10",
  "structure.minecraft.desert_pyramid.stay": "60",
  "structure.minecraft.desert_pyramid.fadeout": "20"
}
```

### 文本样式

| 配置项 | 类型 | 默认值 | 有效值 | 说明 |
|-------|------|--------|-------|------|
| `color` | 字符串 | `FFFFFF` | 6位十六进制 | 标题颜色（如 `FFAA00`） |
| `bold` | 布尔 | `false` | `true`/`false` | 粗体 |
| `italic` | 布尔 | `false` | `true`/`false` | 斜体 |
| `underline` | 布尔 | `false` | `true`/`false` | 下划线 |
| `strikethrough` | 布尔 | `false` | `true`/`false` | 删除线 |
| `shadow` | 布尔 | `true` | `true`/`false` | 字体阴影（设为 `false` 可禁用阴影） |

```json
{
  "structure.minecraft.desert_pyramid.color": "FFAA00",
  "structure.minecraft.desert_pyramid.bold": "true",
  "structure.minecraft.desert_pyramid.italic": "false",
  "structure.minecraft.desert_pyramid.shadow": "false"
}
```

**禁用文字阴影：**
```json
{
  "structure.minecraft.desert_pyramid.shadow": "false"
}
```

### 渲染设置

| 配置项 | 类型 | 默认值 | 有效范围 | 说明 |
|-------|------|--------|---------|------|
| `opacity` | 整数 | `100` | 0-100 | 不透明度（%） |
| `scale` | 整数 | `100` | 25-400 | 缩放比例（%，100=原版大小） |
| `posx` | 整数 | `0` | -1000~1000 | X轴偏移（像素，负数向左，正数向右） |
| `posy` | 整数 | `0` | -1000~1000 | Y轴偏移（像素，负数向上，正数向下） |

```json
{
  "structure.minecraft.desert_pyramid.opacity": "80",
  "structure.minecraft.desert_pyramid.scale": "120",
  "structure.minecraft.desert_pyramid.posx": "0",
  "structure.minecraft.desert_pyramid.posy": "-10"
}
```

### 音效设置

| 配置项 | 类型 | 默认值 | 说明 |
|-------|------|--------|------|
| `sound` | 字符串 | 全局配置 | 音效ID，空字符串禁用 |
| `volume` | 整数 | `10` | 0-100，音量百分比 |

```json
{
  "structure.minecraft.desert_pyramid.sound": "minecraft:block.note_block.pling",
  "structure.minecraft.desert_pyramid.volume": "50"
}
```

**常用音效ID：**
- `entity.experience_orb.pickup` - 经验球（默认）
- `block.note_block.pling` - 音符盒
- `ambient.sculk_charge` - 幽匿尖啸
- `entity.player.levelup` - 升级
- `ui.toast.challenge_complete` - 成就
- `block.beacon.power_select` - 信标
- `entity.ender_dragon.growl` - 末影龙咆哮

**禁用音效：**
```json
{
  "structure.minecraft.stronghold.sound": "",
  "structure.minecraft.stronghold.volume": "0"
}
```

### 标题与副标题分开设置

默认情况下，样式设置同时应用于主标题和副标题。你可以通过 `title.` 和 `subtitle.` 前缀为它们分别设置不同样式：

| 分开设置格式 | 说明 |
|-------------|------|
| `structure.<ns>.<path>.title.<属性>` | 仅应用于主标题 |
| `structure.<ns>.<path>.subtitle.<属性>` | 仅应用于副标题 |

**支持的分开设置属性：**

| 属性 | 类型 | 说明 |
|------|------|------|
| `title.color` / `subtitle.color` | 字符串 | 标题/副标题独立颜色 |
| `title.opacity` / `subtitle.opacity` | 整数 | 标题/副标题独立不透明度 |
| `title.scale` / `subtitle.scale` | 整数 | 标题/副标题独立缩放 |
| `title.posx` / `subtitle.posx` | 整数 | 标题/副标题独立X偏移 |
| `title.posy` / `subtitle.posy` | 整数 | 标题/副标题独立Y偏移 |
| `title.shadow` / `subtitle.shadow` | 布尔 | 标题/副标题独立阴影 |
| `title.fadein` / `subtitle.fadein` | 整数 | 标题/副标题独立淡入时间 |
| `title.stay` / `subtitle.stay` | 整数 | 标题/副标题独立保持时间 |
| `title.fadeout` / `subtitle.fadeout` | 整数 | 标题/副标题独立淡出时间 |

**优先级：** `title.xxx` > `xxx`（统一设置） > 全局/默认值

```json
{
  "structure.minecraft.ancient_city": "远古城市",
  "structure.minecraft.ancient_city.title.color": "FF5555",
  "structure.minecraft.ancient_city.title.bold": "true",
  "structure.minecraft.ancient_city.title.shadow": "false",
  "structure.minecraft.ancient_city.subtitle.color": "AAAAAA",
  "structure.minecraft.ancient_city.subtitle.opacity": "80"
}
```

> 上面示例中：主标题为红色粗体且无阴影，副标题为灰色半透明。

---

### 自定义颜色

#### 维度颜色

副标题中的维度名称可以自定义颜色：

| 配置项 | 默认颜色 | 说明 |
|-------|---------|------|
| `firststeps.overworld.color` | `55FF55` | 主世界名称颜色（绿色） |
| `firststeps.the_nether.color` | `FF5555` | 下界名称颜色（红色） |
| `firststeps.the_end.color` | `AA00AA` | 末地名称颜色（紫色） |
| `firststeps.unknown_dimension.color` | `AAAAAA` | 未知维度名称颜色（灰色） |

```json
{
  "firststeps.overworld.color": "55FF55",
  "firststeps.the_nether.color": "FF5555",
  "firststeps.the_end.color": "AA00AA"
}
```

#### 模组前缀颜色

当启用"显示模组前缀"时，可以自定义每个模组的前缀颜色：

| 配置项 | 默认颜色 | 说明 |
|-------|---------|------|
| `firststeps.prefix.color` | `FFAA00` | 默认前缀颜色（金色） |
| `firststeps.prefix.minecraft.color` | `FFAA00` | Minecraft 原版前缀颜色 |
| `firststeps.prefix.terralith.color` | `00AAAA` | Terralith 前缀颜色 |
| `firststeps.prefix.qraftyfied.color` | `AA00AA` | Qraftyfied 前缀颜色 |
| `firststeps.prefix.qrafty.color` | `AA00AA` | Qrafty 前缀颜色 |
| `firststeps.prefix.repurposed_structures.color` | `AA5500` | Repurposed Structures 前缀颜色 |

```json
{
  "firststeps.prefix.color": "FFAA00",
  "firststeps.prefix.terralith.color": "00AAAA",
  "firststeps.prefix.mymod.color": "FF00FF"
}
```

> 任何模组都可以通过 `firststeps.prefix.<模组ID>.color` 设置前缀颜色。

#### 维度名称翻译

维度名称也可以自定义翻译：

| 配置项 | 默认值 |
|-------|--------|
| `firststeps.overworld` | `Overworld` / `主世界` |
| `firststeps.the_nether` | `The Nether` / `下界` |
| `firststeps.the_end` | `The End` / `末地` |
| `firststeps.unknown_dimension` | `Unknown Dimension` / `未知维度` |

---

### 全局样式（Lang文件）

除了为每个结构单独配置样式外，还可以通过全局样式键为**所有结构**设置默认样式。当结构特定键不存在时，会回退到全局键。

#### 全局样式键格式

| 格式 | 说明 |
|------|------|
| `firststeps.global.<属性>` | 全局统一设置（标题和副标题都适用） |
| `firststeps.global.title.<属性>` | 全局主标题特定设置 |
| `firststeps.global.subtitle.<属性>` | 全局副标题特定设置 |

#### 支持的全局属性

| 属性 | 类型 | 说明 |
|------|------|------|
| `color` | 字符串 | 全局颜色 |
| `opacity` | 整数 | 全局不透明度 |
| `scale` | 整数 | 全局缩放 |
| `posx` | 整数 | 全局X偏移 |
| `posy` | 整数 | 全局Y偏移 |
| `shadow` | 布尔 | 全局阴影 |
| `bold` | 布尔 | 全局粗体 |
| `italic` | 布尔 | 全局斜体 |
| `fadein` | 整数 | 全局淡入时间 |
| `stay` | 整数 | 全局保持时间 |
| `fadeout` | 整数 | 全局淡出时间 |
| `volume` | 整数 | 全局音量 |

**示例 - 全局禁用阴影并设置默认颜色：**

```json
{
  "firststeps.global.shadow": "false",
  "firststeps.global.color": "FFAA00",
  "firststeps.global.title.bold": "true",
  "firststeps.global.subtitle.opacity": "80",
  "firststeps.global.volume": "30"
}
```

> 上面示例中：所有结构默认无阴影、金色标题，主标题粗体，副标题80%不透明度，音量30%。

---

## 完整示例

### 示例1：沙漠神殿 - 金色标题，特殊音效

```json
{
  "structure.minecraft.desert_pyramid": "沙漠神殿",
  "structure.minecraft.desert_pyramid.color": "FFAA00",
  "structure.minecraft.desert_pyramid.bold": "true",
  "structure.minecraft.desert_pyramid.scale": "120",
  "structure.minecraft.desert_pyramid.sound": "minecraft:block.note_block.pling",
  "structure.minecraft.desert_pyramid.volume": "50"
}
```

### 示例2：远古城市 - 紫色斜体，恐怖音效，低音量

```json
{
  "structure.minecraft.ancient_city": "远古城市",
  "structure.minecraft.ancient_city.color": "AA00AA",
  "structure.minecraft.ancient_city.italic": "true",
  "structure.minecraft.ancient_city.opacity": "70",
  "structure.minecraft.ancient_city.sound": "minecraft:ambient.sculk_charge",
  "structure.minecraft.ancient_city.volume": "20"
}
```

### 示例3：要塞 - 只显示副标题，静音

```json
{
  "structure.minecraft.stronghold": "要塞",
  "structure.minecraft.stronghold.showtitle": "false",
  "structure.minecraft.stronghold.showsubtitle": "true",
  "structure.minecraft.stronghold.sound": "",
  "structure.minecraft.stronghold.volume": "0"
}
```

### 示例4：林地府邸 - 完整自定义

```json
{
  "structure.minecraft.mansion": "林地府邸",
  "structure.minecraft.mansion.color": "55FF55",
  "structure.minecraft.mansion.bold": "true",
  "structure.minecraft.mansion.italic": "true",
  "structure.minecraft.mansion.opacity": "90",
  "structure.minecraft.mansion.scale": "110",
  "structure.minecraft.mansion.posy": "-5",
  "structure.minecraft.mansion.fadein": "15",
  "structure.minecraft.mansion.stay": "80",
  "structure.minecraft.mansion.fadeout": "25",
  "structure.minecraft.mansion.sound": "entity.ender_dragon.growl",
  "structure.minecraft.mansion.volume": "30"
}
```

### 示例5：多个结构批量配置

```json
{
  "_comment_desert": "沙漠结构",
  "structure.minecraft.desert_pyramid.color": "FFAA00",
  "structure.minecraft.desert_pyramid.bold": "true",

  "_comment_jungle": "丛林结构",
  "structure.minecraft.jungle_pyramid.color": "00AA00",
  "structure.minecraft.jungle_pyramid.italic": "true",

  "_comment_ice": "雪地结构",
  "structure.minecraft.igloo.color": "AAAAFF",
  "structure.minecraft.igloo.sound": "block.snow.place"
}
```

---

## 故障排除

### 配置不生效

1. **检查JSON格式**
   - 确保使用英文双引号 `"`
   - 确保最后一项没有逗号
   - 使用在线JSON验证器检查

2. **检查文件位置**
   - 确认文件在 `assets/firststeps/lang/` 目录下
   - 确认文件名正确（如 `zh_cn.json`, `en_us.json`）

3. **检查结构ID**
   - 在游戏中按F3确认结构ID
   - 注意命名空间和路径的拼写

### 输入保护机制

模组已内置输入保护，以下情况会自动使用默认值：

| 配置项 | 无效输入示例 | 自动恢复为 |
|-------|------------|-----------|
| `color` | `GGG`, `#FFAA00` | `FFFFFF` |
| `opacity` | `150`, `-10` | `100` |
| `scale` | `500`, `10` | `100` |
| `posx/posy` | `9999`, `-9999` | `0` |
| `fadein/stay/fadeout` | `99999`, `-5` | 默认值 |
| `bold/italic/underline/strikethrough` | `yes`, `1` | `false` |
| `show/showtitle/showsubtitle` | `enabled`, `2` | `true` |

### 音效不播放

1. 在游戏中测试音效ID：`/playsound <音效ID> master @s`
2. 检查音量是否为0或空字符串
3. 检查游戏音量设置

### 标题不显示

1. 检查 `show` 是否设置为 `false`
2. 检查 `showtitle` 是否设置为 `false`
3. 检查 `opacity` 是否为0
4. 检查 `scale` 是否太小（<25会被重置为100）
5. 检查结构是否有翻译键

---

## 服务器端样式同步

当连接到安装了First Steps的服务器时，服务器可以覆盖客户端的样式配置。

### 工作原理

1. 玩家加入服务器时，服务器发送所有样式覆盖
2. 客户端优先使用服务器的样式配置
3. 断开连接后恢复客户端原始配置

### 服务器配置

在服务器端的语言文件中添加样式键（与客户端相同格式）：

```json
{
  "structure.minecraft.desert_pyramid.color": "FF0000",
  "structure.minecraft.desert_pyramid.bold": "true"
}
```

### 优先级

```
服务器样式（多人游戏） > 结构特定配置（Lang文件） > 全局Lang样式 > 全局配置（ModMenu/JSON） > 模组默认值
```

---

## 配置优先级总结

对于每个样式属性（如颜色、阴影等），完整查找优先级从高到低：

```
1. 服务器覆盖 — structure.<ns>.<path>.title.<属性>   （主标题特定）
2. 服务器覆盖 — structure.<ns>.<path>.<属性>          （统一设置）
3. Lang文件  — structure.<ns>.<path>.title.<属性>     （主标题特定）
4. Lang文件  — structure.<ns>.<path>.<属性>            （统一设置）
5. Lang全局  — firststeps.global.title.<属性>          （全局主标题特定）
6. Lang全局  — firststeps.global.subtitle.<属性>       （仅副标题适用）
7. Lang全局  — firststeps.global.<属性>                （全局统一设置）
8. ModConfig 默认值 (config/firststeps.json)
```

> 对于副标题，步骤 1/3 会查找 `subtitle.<属性>` 而非 `title.<属性>`。

简化版：

```
服务器样式（多人游戏）
    ↓
结构特定配置（Lang文件：title.xxx > xxx）
    ↓
全局Lang样式（firststeps.global.title.xxx > firststeps.global.subtitle.xxx > firststeps.global.xxx）
    ↓
全局配置（ModMenu/JSON文件）
    ↓
模组默认值
```

示例：
- 全局配置音量：30
- 沙漠神殿特定音量：50
- 服务器配置音量：80
- 结果：进入沙漠神殿时音量80（服务器优先）

---

**版本：** 0.98  
**最后更新：** 2026-04-13  
**支持MC版本：** 1.21 - 1.21.6+
