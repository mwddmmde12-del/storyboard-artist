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

**核心原则：Veo 用结构化精确控制，即梦用电影化叙事驱动。两套提示词风格完全不同，不可混用。**

---

#### 🎬 Veo 3.1 英文提示词：五维结构化法

Veo 3.1 需要像导演写技术方案一样精确。每次生成必须覆盖以下 5 个维度：

**五维公式：`摄影镜头构图 + 主体规范 + 动作与物理交互 + 环境与氛围 + 风格美学`**

**维度 1：摄影与镜头构图（Cinematography）**
- 必须指定：镜头类型（camera_type）、运镜方式（movement）、焦距（focal_length）、光圈（aperture）
- 运镜使用专业术语：`slow dolly in`, `handheld tracking shot`, `aerial crane shot`, `180-degree arc shot`, `anamorphic lens`
- 速度分级：`very_slow`, `slow`, `medium`, `fast`, `very_fast`
- 有效运镜类型枚举：`static`, `pan_left`, `pan_right`, `tilt_up`, `tilt_down`, `truck_left`, `truck_right`, `dolly_in`, `dolly_out`, `descend`, `ascend`, `push_in`, `pull_out`, `orbit_cw`, `orbit_ccw`

**维度 2：主体规范（Subject）**
- 对每个角色必须极其具体：年龄、种族、服装材质、发型、面部特征、皮肤纹理
- 禁止用角色名字，必须用外貌描述保持一致性
- 高频有效词：`grizzled`（沧桑感）, `expressive wide eyes`（情感连接）, `weathered skin`（阅历感）

**维度 3：动作与物理交互（Action & Physics）**
- 不只说"做什么"，必须描述"如何做"以及物理后果
- 必须包含至少一个物理细节：`explosion of flour`, `condensation forming on glass`, `steam rising`, `cloth fluttering in wind`
- 动态细节示例：不说"修补渔网"，说"用布满伤疤的手一针一线修补渔网，指尖被麻绳勒出红痕"

**维度 4：环境与氛围（Environment）**
- 光线具体化：`golden hour backlight`, `harsh overhead lighting`, `soft diffused natural light`, `neon-lit cyberpunk alley`
- 天气与氛围：`fog-drenched`（悬疑）, `dappled sunlight`（自然）, `volumetric rays`（神圣）
- 构图引用：`rule of thirds`, `Dutch angle`, `symmetrical composition`, `shallow depth of field`

**维度 5：风格与美学（Style & Aesthetics）**
- 风格指令：`cinematic film grain`, `hyper-realistic`, `VHS footage`, `noir`, `Pixar-style 3D animation`
- 导演风格：`in the style of [Director]`
- 美术风格：`[Style] aesthetic`
- 必须标注帧率和画幅：`24fps`, `16:9`, `anamorphic`

**Veo 3.1 提示词模板（每个镜头都必须按此结构生成）：**

```
[Cinematography] [Shot Size] shot, [Camera Movement] at [Speed] speed, [Focal Length] lens, [Aperture] aperture.

[Subject] [Detailed character appearance with clothing material, hair, skin texture, age], [Specific action with physical consequences and micro-details].

[Environment] Set in [Detailed location description], [Time of day] lighting with [Specific light source and direction], [Weather/atmosphere], [Mood keyword].

[Style] [Visual style], [Color grading], [Film grain/textures], [Director reference if any].

[Negative] Avoid: [List of unwanted elements]
```

**Veo 3.1 完整示例：**
> Medium close-up shot, slow push-in at slow speed, 85mm lens, f/1.8 aperture. A man in his late 30s with deep brown skin, short cropped hair, wearing a faded yellow Danfo bus driver's t-shirt, sits by the window. His brow furrows as he stares intently at his phone screen, then his pupils dilate, the corners of his mouth twitch upward before breaking into a wide grin. He leaps to his feet, clutching the phone with both trembling hands. Set inside a crowded Lagos yellow Danfo bus, harsh afternoon tropical sunlight streaming through dusty windows casting dramatic shadows, warm orange interior light contrasting with bright exterior. Cinematic, warm color palette with golden highlights, subtle film grain, 24fps, 16:9. Avoid: cartoon, anime, low quality, distorted faces.

---

#### 🌙 即梦 Seedance 2.0 中文提示词：电影化叙事法

即梦 Seedance 2.0 的核心是**讲故事**。提示词不是参数清单，而是一段有情节推进、情绪转折、动作细节的微型剧本。

**核心公式：`场景 + 人物 + 情绪变化弧线 + 具体动作序列 + 环境感官细节 + 镜头感觉`**

**关键原则：**

1. **叙事优先，参数第二**：先想清楚"这个镜头讲什么故事"，再补充镜头参数
2. **情绪弧线是灵魂**：每个提示词必须有清晰的情绪变化，用逗号分隔的动词链推动情绪
   - 情绪动词链示例：`一脸紧张地凝视 → 皱起眉头 → 瞳孔收缩 → 嘴角上扬 → 突然开怀大笑`
3. **动作要微观具体**：不说"看手机"，说"双手紧握手机，指尖发白，屏幕的光映在他的瞳孔里"
4. **环境要有感官**：加入声音暗示、温度暗示、气味暗示
   - 声音暗示：`引擎的轰鸣声`, `车窗外嘈杂的街道噪音`
   - 温度暗示：`闷热潮湿的热带午后`
   - 气味暗示：`空气中弥漫着柴油和汗水混合的味道`
5. **对白直接嵌入**：即梦支持文字渲染，对话直接写在提示词中用引号标注
6. **群体反应增加戏剧性**：不只有主角反应，还要写周围人的连锁反应
7. **结尾要有冲击力**：最后一个画面必须有记忆点

**即梦提示词结构模板：**

```
[场景环境描述，包含感官细节],

[人物外貌和状态描述],

[动作序列：起始状态 → 情绪转变 → 高潮动作，用"→"或逗号串联],

[对白，用引号直接写入],

[群体/环境连锁反应],

[结尾冲击画面]
```

**即梦 Seedance 2.0 完整示例：**
> 在尼日利亚拉各斯的闷热午后，一辆破旧的黄色Danfo公交车在坑坑洼洼的土路上颠簸，车厢里弥漫着柴油和汗水混合的味道，引擎发出嘶哑的轰鸣，一个坐在窗边的黑人青年，穿着褪色的蓝色T恤，一脸紧张地盯着自己的手机屏幕，他仔细凝视了一会儿，眉头紧锁，突然瞳孔骤然收缩，嘴角不受控制地上扬，猛然间开怀大笑，对着全车的人大声喊叫「I just won 100 million naira!!!」，车内的乘客纷纷从座位上弹起，蜂拥着挤过来看他的手机，一群人疯狂地追问：Where did you win？黑人青年激动地回答：WajeGame! Guys! WajeGame! 全车人瞬间沸腾，有人拍打座椅，有人高举双手欢呼，车窗外的拉各斯街头依旧嘈杂，但此刻车厢内仿佛成了全世界最快乐的地方

**即梦 vs Veo 提示词对比（同一个镜头）：**

| 维度 | Veo 3.1（结构化） | 即梦 Seedance 2.0（叙事化） |
|------|-------------------|---------------------------|
| 开头 | 镜头参数：景别+运镜+焦距 | 场景环境+感官氛围 |
| 人物 | 外貌参数：年龄+种族+服装材质 | 人物状态+情绪描写 |
| 动作 | 物理动作+微观细节 | 情绪弧线+动词链 |
| 对白 | 在 subject 区域标注 | 直接嵌入叙事流 |
| 光影 | 精确光源+方向+色温 | 融入环境氛围描写 |
| 结尾 | negative prompts | 群体反应+冲击画面 |

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
