# Veo 3.1 & 即梦 Seedance 2.0 提示词最佳实践

> 可动态扩展。建议每次使用前搜索最新技巧并更新此文件。

## Veo 3.1 提示词规则

### 结构模板
[Shot Type], [Camera Movement], [Subject + Action], [Environment], [Lighting], [Composition], [Color/Mood], [Style Reference], [Technical Specs]

### 最佳实践
1. **英文必须专业准确**：使用行业标准术语
2. **镜头语言优先**：先说景别和运镜
3. **光影具体化**：不要说"nice lighting"，要说"golden hour backlight through dusty window"
4. **动作要具体**：不要说"walks"，要说"slowly walks with hands in pockets"
5. **避免角色名**：用外貌描述替代
6. **风格参考放后面**：in the style of [Director] 或 [Film] aesthetic
7. **技术参数可选**：24fps, 35mm, anamorphic, film grain

### 提示词示例
Wide establishing shot, slow crane up, a lone figure stands at the edge of a cliff overlooking a vast desert canyon, golden hour sidelight casting long shadows, rule of thirds composition, warm amber and dusty rose color palette, cinematic film grain, in the style of Denis Villeneuve, 24fps, anamorphic lens

### 常见问题
- 错误: "a man walks in a city" \u2192 正确: "medium tracking shot, a man in a grey overcoat walks through rain-soaked Tokyo streets at night"
- 错误: "scary scene" \u2192 正确: "Dutch angle close-up, a woman terrified face illuminated by flickering fluorescent light, cold blue-green color palette"
- 错误: "beautiful sunset" \u2192 正确: "wide static shot, sun setting over calm ocean, warm golden and pink gradient sky, soft waves reflecting orange light"

## 即梦 Seedance 2.0 提示词规则

### 结构模板
[风格标签], [景别+运镜], [画面主体+动作], [环境+氛围], [色调+光影], [技法标签]

### 最佳实践
1. **中文描述要画面感强**：像一个画家在描述画面
2. **风格标签放最前面**：即梦对首部关键词敏感
3. **使用即梦擅长理解的关键词**：电影质感、德味、日系清新、胶片质感、暗黑童话
4. **导演风格可以直接引用**：王家卫风格、诺兰风格
5. **技法可以直接引用**：眩晕变焦、一镜到底、荷兰角
6. **情绪用氛围词表达**：孤独、暧昧、紧张感、仪式感
7. **色彩描述要具体**：暖橙色、冷蓝色调、霓虹紫

### 提示词示例
电影质感，大全景缓推，一个穿灰色风衣的男人独自站在悬崖边俯瞰峡谷，黄昏侧光投射长影，三分法构图，暖琥珀与玫瑰色调，胶片颗粒感，维伦纽瓦风格

### 即梦 Seedance 2.0 特殊技巧
- **风格化效果强**：Seedance 2.0 对风格标签特别敏感，多用
- **导演/影片风格**：直接说"沙丘风格""Arcane风格"效果很好
- **角色一致性**：通过服装+发型+体态组合维持
- **运动流畅度**：即梦对运动描述的理解力强，充分利用
- **画面细节**：可以描述更多环境细节

## 双平台差异对照

| 维度 | Veo 3.1 | 即梦 Seedance 2.0 |
|------|---------|------------------|
| 语言 | 英文 | 中文 |
| 核心优势 | 镜头语言+光影 | 风格化+画面氛围 |
| 运镜描述 | 专业术语 | 中文描述即可 |
| 风格参考 | in the style of [Director] | 直接说风格名 |
| 人物一致性 | 外貌描述 | 外貌描述 |
| 光影描述 | 非常具体 | 可以抽象一些 |
| 最佳长度 | 50-150词 | 30-80字 |

## 更新日志
<!-- 首次创建: 2026-03-30 -->
