# Minecraft 指令师（Minecraft Instructional Designer）

> 面向《我的世界》**Java 版 1.21.x** 的 AI 指令技能包。让 AI 助手输出**语法准确、可直接使用**的指令、命令方块与数据包函数。

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)

## 📖 这是什么

这是一个 **AI 技能包（Skill）**——一段结构化的系统提示词，用于把 AI 助手（如游戏内 AI 对话 Mod、通用大模型对话）训练成一名《我的世界》Java 版资深指令与数据包工程师。

当用户提出"给我一个 XX 的指令 / 做一个每日任务 / 设计一个机关 / 手持雪球加速"之类的需求时，技能会让 AI：

- 输出**语法准确、可直接复制使用**的 Java 版 1.21.x 指令；
- **绝不编造语法**——不确定的命令明确标注"请在测试世界验证"，宁可少给不可给错；
- 区分**状态效果与附魔**、**数据组件与旧 NBT**、**命令方块与函数**等易错概念；
- 涉及危险指令（`/kill @a` 等）时主动警告并给出安全写法。

## ✨ 特性

- **10 条输出纪律**：红线级约束，从源头杜绝基岩版混入、旧 NBT、错误附魔、幻觉语法
- **核心语法速查**：`execute` 链式写法、选择器、记分板、物品组件（1.20.5+），易错点全部 ⚠ 标注
- **输出前自查清单**：8 项强制检查，AI 每条回复输出前逐条核对
- **4 个高质量功能模板**：每日任务系统、区域触发机关、技能冷却、手持物品触发效果（命令方块版 + tick 函数版，均经语法校核）
- **性能与安全红线**：20Hz 循环成本、选择器过滤、命令长度限制等实战经验

## 📂 目录结构

```
mcai-minecraft-instructional-designer/
├── Minecraft-Instructional-Designer/
│   └── SKILL.md          # 技能正文（含 YAML 头：name / description / license）
└── README.md             # 本文件
```

## 🚀 使用方法

### 方式一：配合 mc-ai-assistant Mod（游戏内 AI 助手）

1. 下载本技能包的 `Minecraft-Instructional-Designer/SKILL.md`
2. 放入游戏配置目录（PCL2 版本隔离示例）：
   ```
   <你的 .minecraft>/versions/<版本>/config/mcai/skills/Minecraft-Instructional-Designer/SKILL.md
   ```
3. 重启游戏，AI 助手即自动加载该技能（用户自定义技能优先于 Mod 内置）

### 方式二：作为提示词直接给任意 AI

将 `SKILL.md` 的内容作为 system prompt（或粘贴在对话开头）发给任意支持长上下文的 AI 即可。

### 方式三：导入技能市场 / 技能平台

`SKILL.md` 顶部含标准 YAML 头（`name` / `description` / `license`），可直接用于支持该格式的技能市场或 WorkBuddy 等平台的技能目录。

## ⚙️ 适用版本

| 项目 | 版本 |
|------|------|
| Minecraft Java 版 | **1.21.x**（1.21 ~ 1.21.8 语法一致） |
| 数据包格式 | `pack_format 48`，`supported_formats [48, 81]`（1.21.9+ 用 `min_format:88, max_format:88`） |
| 物品系统 | 1.20.5+ 数据组件（**禁止**旧 NBT 物品格式） |

## 📌 典型能力示例

| 需求 | 正确做法 |
|------|----------|
| 锋利 255 的木棍 | `give @p stick[enchantments={levels:{"minecraft:sharpness":255}}] 1` |
| 手持雪球加速 | 每刻检测主手物品 + 施加/撤销 `minecraft:speed` 状态效果（**不是**附魔） |
| 每日任务 | 数据包 tick 检测游戏日变化 + 统计进度 + `/trigger` 领奖 |
| 区域欢迎横幅 | 循环命令方块 + `if entity @a[tag=!welcomed]` + `title` |
| 技能冷却 | 记分板 `cd` 倒计时 + `trigger` 施法 |

## 📜 许可证

[MIT](LICENSE)

---

*本项目为 mc-ai-assistant（Minecraft 游戏内 AI 对话 Mod）的内置技能包独立发布版。*
