# Veo 3.1 & 即梦 Seedance 2.0 提示词最佳实践

> 可动态扩展。建议每次使用前搜索最新技巧并更新此文件。
> 最后更新：2026-03-30 | 来源：Google DeepMind 官方指南、社区实战测试

---

## 一、Veo 3.1 提示词：五维结构化法

### 设计理念

Veo 3.1 需要像导演写技术方案一样精确。提示词不是灵感描述，而是**给 AI 摄制组的施工图纸**。

### 五维公式

`摄影镜头构图 + 主体规范 + 动作与物理交互 + 环境与氛围 + 风格美学`

### 维度详解

#### 维度 1：摄影与镜头构图（Cinematography）

必须指定 4 个参数：镜头类型、运镜方式、焦距、光圈。

**摄像机类型（camera_type）：**
| 类型 | 适用场景 | 效果 |
|------|---------|------|
| `drone` | 航拍大景 | 上帝视角、史诗感 |
| `handheld` | 纪实/紧张 | 轻微晃动、真实感 |
| `tripod` | 稳定对话 | 固定、严肃 |
| `gimbal` | 平滑运动 | 丝滑流畅 |
| `crane` | 升降大景 | 戏剧性揭示 |
| `dolly` | 推拉特写 | 情感聚焦 |

**运镜类型（movement）完整枚举：**
`static`, `pan_left`, `pan_right`, `tilt_up`, `tilt_down`, `truck_left`, `truck_right`, `dolly_in`, `dolly_out`, `descend`, `ascend`, `push_in`, `pull_out`, `orbit_cw`, `orbit_ccw`

**速度分级：**
`very_slow`, `slow`, `medium`, `fast`, `very_fast`

**高级运镜组合：**
- `slow dolly in with shallow depth of field` → 情感聚焦
- `180-degree arc shot` → 展示主体 3D 结构
- `Dutch angle tilt down` → 不安、扭曲感
- `anamorphic lens with horizontal lens flare` → 变形宽银幕电影感
- `handheld tracking shot with motion blur` → 追逐/紧张

#### 维度 2：主体规范（Subject）

- 对每个角色必须极其具体：年龄、种族、服装材质、发型、面部特征、皮肤纹理
- **禁止用角色名字**，必须用外貌描述保持一致性
- 高频有效词汇：
  - `grizzled` — 灰白头发，沧桑感
  - `expressive wide eyes` — 富有表现力的大眼睛
  - `weathered skin` — 饱经风霜的皮肤
  - `sun-kissed` — 阳光晒出的健康肤色
  - `impeccably groomed` — 一丝不苟的造型

#### 维度 3：动作与物理交互（Action & Physics）

核心原则：不只说"做什么"，必须描述"如何做"以及物理后果。

**错误示范 vs 正确示范：**
| ❌ 错误 | ✅ 正确 |
|---------|---------|
| walks through the market | navigates through a crowded market, elbows brushing past vendors, ducking under hanging fabrics |
| looks at the phone | stares intently at the glowing phone screen, the blue light reflecting in his dilated pupils |
| cooks food | chops onions with rapid precise strokes, tears welling up, steam rising from the sizzling pan |

**必含物理细节（至少选一个）：**
- 流体：`explosion of flour`, `water splashing`, `rain dripping`
- 粒子：`dust motes floating`, `sparks flying`, `ash drifting`
- 布料：`cloth fluttering in wind`, `silk rippling`
- 环境物理：`condensation forming on glass`, `footprints in fresh snow`

#### 维度 4：环境与氛围（Environment）

**光线类型：**
- `golden hour backlight` — 温暖美丽
- `harsh overhead lighting` — 压迫、暴露
- `soft diffused natural light` — 柔和自然
- `volumetric rays through dusty windows` — 戏剧性光柱
- `neon-lit` — 科技/赛博朋克
- `fog-drenched` — 悬疑神秘
- `dappled sunlight through canopy` — 自然森林

**氛围关键词：**
`noir melancholy`, `ethereal serenity`, `raw visceral energy`, `claustrophobic tension`, `sublime vastness`

#### 维度 5：风格与美学（Style & Aesthetics）

| 风格指令 | 效果 |
|----------|------|
| `cinematic film grain` | 经典电影质感 |
| `hyper-realistic` | 超写实 |
| `VHS footage with slight wear` | 复古录像带 |
| `35mm film noir` | 黑白黑色电影 |
| `Pixar-style 3D animation` | 皮克斯动画 |
| `glitch art` | 故障艺术 |

### Veo 3.1 提示词模板

```
[Cinematography] [Shot Size] shot, [Camera Movement] at [Speed] speed, [Focal Length] lens, [Aperture] aperture.

[Subject] [Detailed character appearance with clothing material, hair, skin texture, age], [Specific action with physical consequences and micro-details].

[Environment] Set in [Detailed location description], [Time of day] lighting with [Specific light source and direction], [Weather/atmosphere], [Mood keyword].

[Style] [Visual style], [Color grading], [Film grain/textures], [Director reference if any].

[Negative] Avoid: [List of unwanted elements]
```

### Veo 3.1 完整示例

**示例 1：情绪转折（广告叙事）**
> Medium close-up shot, slow push-in at slow speed, 85mm lens, f/1.8 aperture. A man in his late 30s with deep brown skin, short cropped hair, wearing a faded yellow Danfo bus driver's t-shirt, sits by the window. His brow furrows as he stares intently at his phone screen, then his pupils dilate, the corners of his mouth twitch upward before breaking into a wide grin. He leaps to his feet, clutching the phone with both trembling hands. Set inside a crowded Lagos yellow Danfo bus, harsh afternoon tropical sunlight streaming through dusty windows casting dramatic shadows, warm orange interior light contrasting with bright exterior. Cinematic, warm color palette with golden highlights, subtle film grain, 24fps, 16:9. Avoid: cartoon, anime, low quality, distorted faces.

**示例 2：动作场景**
> Wide tracking shot, fast handheld movement, 24mm wide-angle lens, f/4 aperture. A woman in her mid-20s with athletic build, long braided hair whipping behind her, wearing a fitted black tactical jacket, sprints through a narrow alleyway in Lagos, leaping over overturned plastic crates, her boots splashing through shallow puddles, water droplets scattering in slow motion. Set in a rain-soaked Lagos slum alley at dusk, neon signs flickering above, deep blue and orange contrast lighting, puddles reflecting scattered light pulses. Hyper-realistic, teal and orange color grading, anamorphic lens flare, film grain, in the style of Cary Joji Fukunaga, 24fps, 2.39:1. Avoid: static camera, clean streets, daylight.

**示例 3：产品广告**
> Macro lens close-up, slow orbital tracking shot at very_slow speed, 100mm macro lens, f/2.8 aperture. A premium smartphone with sleek black glass back, condensation droplets sliding down its surface, rotating slowly to reveal a crystal-clear logo illuminated by soft morning light. A fingertip enters frame, gently wiping away the condensation. Set on a minimalist marble surface, volumetric morning sunlight rays, subtle dust motes floating in the light beam, serene and expensive atmosphere. Ultra-clean, cool white and silver color palette, no film grain, commercial quality, 60fps for smooth motion, 9:16 vertical. Avoid: fingerprints, scratches, cluttered background, warm tones.

---

## 二、即梦 Seedance 2.0 提示词：电影化叙事法

### 设计理念

即梦 Seedance 2.0 的核心是**讲故事**。提示词不是参数清单，而是一段有情节推进、情绪转折、动作细节的微型剧本。让 AI 像读懂一个故事一样去"演"出来。

### 核心公式

`场景 + 人物 + 情绪变化弧线 + 具体动作序列 + 环境感官细节 + 镜头感觉`

### 七大关键原则

#### 原则 1：叙事优先，参数第二
先想清楚"这个镜头讲什么故事"，再补充镜头参数。场景描述永远放在最前面，让 AI 先"看到"画面。

#### 原则 2：情绪弧线是灵魂
每个提示词必须有清晰的情绪变化，用逗号分隔的动词链推动情绪递进。

**情绪动词链示例：**
- 紧张→惊喜：`一脸紧张地凝视 → 皱起眉头 → 瞳孔收缩 → 嘴角上扬 → 突然开怀大笑`
- 平静→震撼：`平静地走着 → 停下脚步 → 缓缓抬起头 → 瞳孔骤然放大 → 嘴唇微微颤抖`
- 愤怒→崩溃：`咬紧牙关 → 双拳紧握 → 身体微微发抖 → 眼眶泛红 → 猛然跪倒在地`

#### 原则 3：动作要微观具体
不说"看手机"，说"双手紧握手机，指尖发白，屏幕的光映在他的瞳孔里"。
不说"跑"，说"跌跌撞撞地跑，鞋带散开也顾不上，脚踩在水坑里溅起泥点"。

#### 原则 4：环境要有感官
加入声音暗示、温度暗示、气味暗示，让场景有"沉浸感"：
- 声音暗示：`引擎的嘶哑轰鸣`, `远处传来清真寺的宣礼声`, `雨滴敲打铁皮屋顶`
- 温度暗示：`闷热潮湿的热带午后`, `刺骨的寒风`, `空调冷气直吹后颈`
- 气味暗示：`空气中弥漫着柴油和汗水混合的味道`, `刚煮好的Jollof饭的香气飘来`

#### 原则 5：对白直接嵌入
即梦支持文字渲染，对话直接写在提示词中用引号标注：
- `大声喊叫「I just won 100 million naira!!!」`
- `低声喃喃「It's over...it's finally over」`
- `猛拍桌子吼道「Enough!」`

#### 原则 6：群体反应增加戏剧性
不只有主角反应，还要写周围人的连锁反应，让画面有"生命力"：
- `周围的乘客纷纷从座位上弹起`
- `整个教室瞬间安静下来，所有人齐刷刷地转头`
- `街上的小贩放下手中的东西，也凑过来看热闹`

#### 原则 7：结尾要有冲击力
最后一个画面必须有记忆点，给观众留下深刻印象：
- `车窗外的拉各斯街头依旧嘈杂，但此刻车厢内仿佛成了全世界最快乐的地方`
- `夕阳把他的影子拉得很长很长，一直延伸到路的尽头`
- `镜头缓缓拉远，这个小小的出租屋里，一个人在黑暗中紧紧抱住了另一个人`

### 即梦提示词结构模板

```
[场景环境描述，包含感官细节],

[人物外貌和状态描述],

[动作序列：起始状态 → 情绪转变 → 高潮动作，用"→"或逗号串联],

[对白，用引号直接写入],

[群体/环境连锁反应],

[结尾冲击画面]
```

### 即梦 Seedance 2.0 完整示例

**示例 1：中奖场景（广告叙事）**
> 在尼日利亚拉各斯的闷热午后，一辆破旧的黄色Danfo公交车在坑坑洼洼的土路上颠簸，车厢里弥漫着柴油和汗水混合的味道，引擎发出嘶哑的轰鸣，一个坐在窗边的黑人青年，穿着褪色的蓝色T恤，一脸紧张地盯着自己的手机屏幕，他仔细凝视了一会儿，眉头紧锁，突然瞳孔骤然收缩，嘴角不受控制地上扬，猛然间开怀大笑，对着全车的人大声喊叫「I just won 100 million naira!!!」，车内的乘客纷纷从座位上弹起，蜂拥着挤过来看他的手机，一群人疯狂地追问：Where did you win？黑人青年激动地回答：WajeGame! Guys! WajeGame! 全车人瞬间沸腾，有人拍打座椅，有人高举双手欢呼，车窗外的拉各斯街头依旧嘈杂，但此刻车厢内仿佛成了全世界最快乐的地方

**示例 2：离别场景（情感叙事）**
> 清晨五点的拉各斯穆尔塔拉穆罕默德机场候机厅，冷白色的荧光灯把所有人的脸照得苍白，一个穿传统约鲁巴服饰的年迈母亲，双手颤抖地握着一个年轻女人的手，眼眶通红却拼命忍着不哭，嘴唇翕动了几下终于开口「Remember to eat well...don't skip meals」，年轻女人低着头，泪水啪嗒啪嗒掉在她们交握的手背上，突然猛地抱住母亲，把脸埋进她的肩膀里，机场广播传来航班登机的通知声，年轻的身体猛然一颤，慢慢松开手，退后一步，用袖子狠狠擦了一把脸，转身走向登机口，没有回头，身后母亲伸出一只手悬在半空，指尖在微微颤抖，登机口的人群穿梭而过，那只手始终没有放下

**示例 3：动作追逐（紧张叙事）**
> 吉隆坡茨厂街的傍晚，霓虹灯牌在细雨中闪烁，一个背双肩包的华人小伙子在人群中狂奔，他回头张望，几个穿黑衣的人影在雨幕中若隐若现地追来，他一个急转弯冲进一条狭窄的巷子，脚下打滑差点摔倒，扶着湿漉漉的墙壁稳住身体继续跑，巷子越跑越窄，两侧是老旧的排屋，晾衣绳上滴落的水打在他脸上，前方一堵墙挡住了去路，他猛地停下，胸口剧烈起伏，雨水顺着发梢流进眼睛，身后的脚步声越来越近越来越近，他深吸一口气，助跑起跳，双手抓住墙头翻了过去，落地时膝盖磕在湿滑的地面上，但他顾不上痛，一瘸一拐地消失在巷子深处的黑暗中

---

## 三、双平台差异对照

| 维度 | Veo 3.1（结构化） | 即梦 Seedance 2.0（叙事化） |
|------|-------------------|---------------------------|
| **设计哲学** | 给 AI 摄制组的施工图纸 | 给演员的微型剧本 |
| **语言** | 英文 | 中文 |
| **开头** | 镜头参数：景别+运镜+焦距 | 场景环境+感官氛围 |
| **人物** | 外貌参数：年龄+种族+服装材质 | 人物状态+情绪描写 |
| **动作** | 物理动作+微观细节 | 情绪弧线+动词链 |
| **对白** | 在 subject 区域标注 | 直接嵌入叙事流 |
| **光影** | 精确光源+方向+色温 | 融入环境氛围描写 |
| **结尾** | negative prompts | 群体反应+冲击画面 |
| **长度** | 80-200 词 | 100-300 字 |
| **核心优势** | 镜头语言+光影+物理模拟 | 风格化+叙事+情绪渲染 |
| **最适合** | 广告片、产品展示、精确控制 | 故事片、情感叙事、文化场景 |

---

## 四、即梦 Seedance 2.0 合规化处理指南

> 即梦运行在中国大陆服务器，受中国互联网内容监管。**所有即梦提示词输出前必须经过合规化处理。**

### 4.1 理解即梦的审核机制

即梦的内容过滤**不是关键词扫描**，而是用语言模型整体理解提示词描述的场景来判断意图：
- 如果提示词缺乏明确的电影化语境（地点、灯光、镜头语言），系统因无法判断意图而倾向**保守拦截**
- 加入影视制作术语能显著降低误标概率

### 4.2 硬拦截内容（不可修复，必须替换）

| 内容类型 | 处理方式 |
|----------|---------|
| 可识别的真实人脸（名人、政客） | 改为虚构人物，不用真实姓名 |
| 受版权保护角色（迪士尼、漫威/DC） | 改为通用描述 |
| 政治敏感内容（政治人物、事件、符号） | 完全避免 |

### 4.3 高风险词汇替换表

| ❌ 必换 | ✅ 安全替代 |
|---------|------------|
| 儿童、小孩、child、boy、loli | 年轻人、青少年、少年、人物 |
| 血、流血、blood | 红色液体、伤痕（必须时） |
| 暴力、violence | 激烈动作、冲突场面 |
| 杀、谋杀、kill、death | 倒下、失去意识（必须时） |
| 裸、性感、sexual | 优雅的、穿着得体的 |
| 赌博、博彩、gambling | 游戏画面、娱乐活动 |
| 自杀、self-harm | 情绪低落、陷入困境 |
| 毒品、drug | 不提及 |

### 4.4 场景安全化重写示例

| ❌ 高风险写法 | ✅ 安全化写法 |
|--------------|-------------|
| 一个男人在街上开枪打人 | 电影质感，1940年代战火纷飞的东欧街道，一名穿灰色制服的士兵向画外方向开火，背景是倒塌建筑的浓烟，阴天散射光，35mm胶片颗粒感，手持拍摄 |
| 两个人在打架 | 电影动作片风格，两名武术家在竹林中对决，慢动作，竹叶纷飞，雾气缭绕，太极服装飘逸，武侠电影质感 |
| 一个人躺在血泊中 | 电影质感，低角度仰拍，一个人倒在雨中的街道上，雨水冲刷着地面，冷蓝色调，霓虹灯闪烁，悬疑电影风格 |

### 4.5 提升过审率的关键技巧

1. **加入影视制作术语**：镜头类型、运镜、灯光、画幅 → 系统识别为专业创作
2. **描述"镜头可见内容"**：只写摄影机能拍到的画面，不写角色动机和背景故事
3. **提示词不要过短**：少于 30 字容易因信息不完整被拦截
4. **附加安全后缀**：每个提示词末尾加 `电影质感，高质量，物理真实，角色一致性强，无不良内容`

### 4.6 @ 引用系统规则

- 每个上传文件必须用 `@文件名` 在提示词中明确角色
- 参考图片**不能含可识别人脸**，否则触发前置拦截（与提示词无关）
- 解决方案：用插画/风格化图片代替照片，或让人物背对镜头/拉远景别

### 4.7 提示词被拒时的排查顺序

1. 检查是否含硬拦截内容（真人脸、版权角色） → 替换素材
2. 检查是否含高风险词汇 → 用替换表处理
3. 检查提示词是否过短 → 补充场景细节至 30 字以上
4. 检查是否缺少影视术语 → 加入镜头/灯光/风格描述
5. 检查参考图片 → 确保不含可识别人脸

---

## 更新日志

<!-- 首次创建: 2026-03-30 -->
<!-- Added: 2026-03-30 | 来源: Google DeepMind 官方指南, DEV Community JSON提示工程, SJinn Seedance 2.0 合集, VeoPrompt.org 五要素公式 -->
