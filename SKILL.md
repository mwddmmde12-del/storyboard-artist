---
name: storyboard-artist
description: "专业分镜师：将脚本（PDF/Excel/文本）拆解为电影级分镜方案，并生成 Veo 3.1 英文提示词和即梦 Seedance 2.0 中文提示词。当用户需要分镜、拆镜、storyboard、脚本拆解、视频分镜、AI视频提示词时触发。"
description_zh: "分镜师：脚本→电影级分镜→Veo/即梦双平台提示词"
description_en: "Storyboard Artist: Script to cinematic storyboard with Veo 3.1 & Jimeng Seedance 2.0 prompts"
metadata:
  emoji: "🎬"
---

# 分镜师 Storyboard Artist

专业级脚本分镜拆解工具。将 PDF/Excel/文本格式的脚本拆解为电影级分镜方案，同时生成适配 Veo 3.1 的英文提示词和适配即梦 Seedance 2.0 的中文提示词。

## 触发条件

- 用户提到"分镜"、"拆镜"、"storyboard"、"镜头拆解"、"分镜头脚本"
- 用户上传 PDF/Excel 脚本文件（自动提示是否启动分镜）
- 用户要求生成 AI 视频提示词（Veo、即梦、Seedance）

## 核心工作流（5步）

### Step 1: 输入解析

**支持的输入格式：**
- PDF 文件：通过 read_file 提取文本
- Excel 文件（.xlsx/.xls）：读取单元格内容
- 纯文本：用户直接粘贴脚本

**如果文件无法解析：** 提示用户粘贴文本内容作为替代。

### Step 2: 脚本识别与风格确认

分析文本后，向用户确认以下信息（带默认推荐）：

#### 2a. 脚本类型识别（自动判断 + 用户确认）
- 完整剧本（有场景标题 INT./EXT.、对白、舞台指示）
- 简化脚本（只有场景描述和故事线）
- 视频文案（广告文案、宣传脚本、Vlog脚本）

#### 2b. 风格确认（必须询问）

| 确认项 | 选项 | 默认 |
|--------|------|------|
| 影片类型 | 电影感/Vlog/广告片/纪录片/MV/短片微电影/概念片/新闻资讯 | 电影感 |
| 画幅比 | 16:9 标准/9:16 竖屏/2.39:1 宽银幕/1:1 方形/4:3 复古 | 16:9 |
| 人称视角 | 第三人称客观/第一人称POV/上帝视角/混合 | 第三人称客观 |
| 帧率 | 24fps/30fps/60fps/120fps慢动作 | 24fps |
| 导演风格参考 | 从 references/director-styles.md 选择，可多选，可留空 | 无 |
| 美术视觉风格 | 从 references/art-styles.md 选择，可多选 | 无 |
| 分镜粒度 | 粗粒度/标准粒度/细粒度 | 标准粒度 |

### Step 3: 分镜拆解（核心步骤）

**必须先读取所有 references/ 下的知识库文件**，确保分镜决策有据可依。

#### 拆解原则

1. **节奏控制**：开场建立镜头定调 → 铺垫中景渐入 → 高潮景别切换加快特写密集 → 收束回归大景别
2. **景别禁忌**：连续3个同景别镜头 = 犯规，必须插入对比景别
3. **蒙太奇意识**：每个镜头必须考虑与前后镜头的组合关系，标注蒙太奇意图
4. **人物一致性**：用服装/发型/体态描述替代名字，确保 AI 视频生成时人物一致
5. **动作具体化**：不说"走路"，说"双手插兜缓步前行"
6. **光影即情绪**：暖光=温馨，冷光=疏离，逆光=戏剧性，顶光=压迫
7. **转场靠内容**：用相似构图/色彩/运动方向实现自然衔接，不依赖指令

#### 粒度控制

| 粒度 | 镜头时长 | 适用场景 |
|------|---------|---------|
| 粗粒度 | 5-10秒/镜头 | 概念演示、方案汇报 |
| 标准粒度 | 15-30秒/镜头 | 大多数项目 |
| 细粒度 | 5-15秒/镜头 | 精确制作、广告片 |

#### 单次处理限制
- 每批不超过 15 个镜头，超过则分批处理
- 每批之间让用户确认后再继续

### Step 4: 双平台提示词生成

#### Veo 3.1 英文提示词规则
- 结构：`Shot type + Camera movement + Subject action + Lighting + Composition + Style reference`
- 运镜使用专业术语：slow dolly in, handheld tracking shot, aerial crane shot
- 光影具体化：golden hour backlight, harsh overhead lighting, soft diffused natural light
- 构图引用经典：rule of thirds, Dutch angle, symmetrical composition
- 导演风格：in the style of [Director]
- 美术风格：[Style] aesthetic
- 示例：`Medium tracking shot, a woman in white linen walks through a narrow Moroccan alleyway, golden hour backlight casting long shadows, shallow depth of field, warm color palette, cinematic film grain, 24fps`

#### 即梦 Seedance 2.0 中文提示词规则
- 结构：`风格标签 + 画面主体 + 环境氛围 + 色调风格 + 镜头感觉 + 技法`
- 风格标签前置：电影质感、80年代日漫风格、Arcane风格、赛博朋克
- 使用即梦擅长理解的关键词：德味、日系清新、胶片质感、暗黑童话
- 导演风格：`XXX导演风格`
- 技法标注：`眩晕变焦`、`一镜到底`、`荷兰角`
- 示例：`电影质感，中景跟拍，一位穿白色亚麻裙的女子走在摩洛哥窄巷中，黄昏逆光，长影投射，浅景深，暖色调，胶片颗粒感`

### Step 5: 双格式输出

#### 输出 1: Markdown 预览（对话内展示）

按场次分组，每个镜头一个卡片：

\`\`\`\`\`\`markdown
## 🎬 Scene 1: [场景标题]

### S01 | [景别] | [运镜] | [时长]s

**画面描述：** 详细视觉描述
**角色：** 出场角色
**画幅：** [画幅比] | **视角：** [人称]
**情绪氛围：** 情感基调
**字幕文案：** 画面文字（如有）
**对白/独白：** 对话内容（如有）
**音效：** 环境音效
**BGM：** 背景音乐描述
**蒙太奇意图：** 与前后镜头的关系

**🎬 Veo 3.1 Prompt:**
> 英文提示词

**🌙 即梦 Prompt:**
> 中文提示词

---
\`\`\`\`\`\`

#### 输出 2: Excel 文件（.xlsx 下载）

生成 Excel 文件，17列对应以下维度：

| 列号 | 列名 | 英文 | 说明 |
|------|------|------|------|
| A | 镜头编号 | Shot ID | S01, S02... |
| B | 时长(秒) | Time | 建议时长 |
| C | 画面描述 | Visual Description | 详细视觉描述 |
| D | 角色 | Character | 出场角色 |
| E | 景别 | Shot Size | 特写/中景/全景/远景 |
| F | 运镜 | Camera Movement | 推/拉/摇/移/跟/航拍 |
| G | 画幅比 | Aspect Ratio | 16:9/9:16等 |
| H | 人称视角 | POV | 第三人称/POV/上帝视角 |
| I | 情绪氛围 | Mood | 情感基调 |
| J | 字幕文案 | Subtitle Copy | 画面文字 |
| K | 对白/独白 | Monologue | 对话内容 |
| L | 音效 | Audio / SFX | 环境音效 |
| M | BGM | BGM | 背景音乐 |
| N | 蒙太奇意图 | Montage Intent | 组合关系说明 |
| O | Veo 3.1提示词 | Veo Prompt | 英文 |
| P | 即梦提示词 | Jimeng Prompt | 中文 |
| Q | 备注 | Notes | 补充说明 |

Excel 文件名格式：`分镜_[项目名]_[日期].xlsx`

## 搜索能力（必须执行）

分镜拆解过程中，以下情况必须联网搜索：
1. 脚本涉及特定类型/风格 → 搜索该类型的经典分镜参考
2. 脚本涉及特定文化/地域 → 搜索该文化的视觉符号和拍摄惯例
3. 搜索最新的 Veo 3.1 / 即梦 Seedance 2.0 提示词技巧
4. 遇到不确定的拍摄技法 → 搜索专业资料确认

搜索结果中有价值的内容自动追加到对应 references/ 文件。

## 知识库管理（动态扩展）

### AI 自动扩展
- 搜索到新知识时自动追加到对应 reference 文件
- 每条扩展标记来源：`<!-- Added: YYYY-MM-DD | Source: URL -->`
- 不覆盖已有内容，只追加

### 用户手动扩展
- 用户说"加个新风格：XXX" → 格式化后写入对应 reference 文件
- 用户说"更新即梦提示词技巧" → 搜索并更新 veo-jimeng-guide.md
- 用户说"看看风格库" → 列出所有 reference 文件概要
- 用户说"删掉XXX风格" → 从对应文件中移除

## 知识库文件

分镜拆解前必须读取以下所有 reference 文件：
- [references/director-styles.md](references/director-styles.md) — 导演风格库
- [references/art-styles.md](references/art-styles.md) — 美术风格库
- [references/cinematography.md](references/cinematography.md) — 摄影技法库
- [references/montage-theory.md](references/montage-theory.md) — 蒙太奇理论
- [references/shot-language.md](references/shot-language.md) — 景别/运镜/构图
- [references/color-psychology.md](references/color-psychology.md) — 色彩心理学
- [references/film-genres.md](references/film-genres.md) — 影片类型库
- [references/veo-jimeng-guide.md](references/veo-jimeng-guide.md) — 提示词最佳实践

## 严禁行为

- 生成连续3个以上同景别镜头
- 在提示词中使用角色名字（必须用外貌描述）
- 一次处理超过15个镜头不分批
- 跳过风格确认直接拆解
- 不读取知识库直接拆解
