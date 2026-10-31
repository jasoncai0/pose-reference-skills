# Pose Reference Skills · 姿势 / 服装 / 人像参考技能包

把 [ai-pose-gallery-zh](https://github.com/anhao/ai-pose-gallery-zh) 的三大图库——1439 张多角度姿势白模图、1407 套服装穿搭、1499 位人像——打包成 8 个**自包含**的 Agent 技能（Agent Skills / `SKILL.md` 格式）。
每个技能包自带全部参考图（WebP），`references/catalog.csv` 用**相对路径**索引，离线可用，不依赖任何外链。

Eight self-contained Agent Skills bundling the pose (1,439), costume (1,407) and portrait (1,499) reference libraries as WebP. Each skill ships its own images; `references/catalog.csv` points to them with paths relative to the skill root.

## 技能列表

| 技能 | 图片数 | 内容 | 体积 |
|-|-:|-|-:|
| [`pose-reference-standard`](skills/pose-reference-standard) | 365 | 全身单人·标准系（站/坐/跪/蹲/趴/扭身等 9 类） | 12 MB |
| [`pose-reference-upper`](skills/pose-reference-upper) | 400 | 上半身单人（可爱/性感/强调系，部分 18+） | 22 MB |
| [`pose-reference-sexy`](skills/pose-reference-sexy) | 399 | 全身单人·性感系（**18+**） | 19 MB |
| [`pose-reference-couple`](skills/pose-reference-couple) | 275 | 双人（**18+**） | 19 MB |
| [`pose-reference-all`](skills/pose-reference-all) | 1439 | 以上全部姿势（含 18+） | 72 MB |
| [`costume-reference`](skills/costume-reference) | 1068 | 服装：春夏秋冬 / 派对礼服 / 泳装度假，按单品、颜色、英文关键词检索 | 25 MB |
| [`costume-reference-sexy`](skills/costume-reference-sexy) | 339 | 服装：内衣睡衣 / 性感穿搭（**18+**） | 8 MB |
| [`portrait-reference`](skills/portrait-reference) | 1499 | 人像：正脸参考 / 造型氛围，4 种发长、51 种发型 | 91 MB |

姿势图有 5 种视角中的若干个：正面 / 斜侧 / 侧面 / 俯视 / 仰视。服装、人像图最长边缩放到 1000px。三类技能可组合：人像定脸和发型 + 服装定穿搭 + 姿势定动作。

## 目录结构

```
skills/pose-reference-standard/
├── SKILL.md                  # 技能说明 + 用法 + 姿势目录
├── references/catalog.csv    # 检索索引；最后一列「图片」= images/<id>.webp（相对技能根目录）
└── images/<id>.webp          # 参考图（随技能打包）
```

## 安装

每个技能目录（`SKILL.md` + `references/` + `images/`）就是一个完整技能包，复制整个目录即可，**不要只复制 `SKILL.md`**。

### 方式一：手动安装

**Claude Code**：个人技能放 `~/.claude/skills/`（所有项目可用），项目技能放 `<项目>/.claude/skills/`（随仓库共享）。

只装一个技能（稀疏克隆，只下载该技能的图片，standard 约 12 MB）：

```bash
git clone --depth 1 --filter=blob:none --sparse https://github.com/jasoncai0/pose-reference-skills.git
cd pose-reference-skills && git sparse-checkout set skills/pose-reference-standard
mkdir -p ~/.claude/skills && cp -r skills/pose-reference-standard ~/.claude/skills/
```

装全部 8 个技能（约 270 MB）：

```bash
git clone --depth 1 https://github.com/jasoncai0/pose-reference-skills.git
mkdir -p ~/.claude/skills && cp -r pose-reference-skills/skills/*-reference* ~/.claude/skills/
```

装好后重启 Claude Code（或新开会话），输入 `/skills` 能看到对应的 `*-reference*` 技能即安装成功。

**其他支持 `SKILL.md` 的 Agent 平台**：把技能目录整个拷到该平台的技能目录，或打包成 zip 后通过平台的「上传技能」入口导入（zip 内保持 `SKILL.md` 在根目录、`images/` 与 `references/` 同级）。

### 方式二：让 Agent 帮你安装

把下面这段话直接发给 Claude Code（或其他能执行命令的 Agent），按需改技能名：

```text
请帮我安装姿势参考技能：从 https://github.com/jasoncai0/pose-reference-skills 稀疏克隆，
只取 skills/pose-reference-standard 目录（含 images/ 和 references/，不要只拷 SKILL.md），
复制到 ~/.claude/skills/pose-reference-standard。完成后列出该目录的 SKILL.md、
references/catalog.csv 和 images/ 下的文件数（应为 365），并确认 catalog.csv 里的图片路径都能找到对应文件。
```

要装其他技能，把技能名换成 `costume-reference` / `portrait-reference` 等；要装全部技能，改成「取 skills/ 下全部 *-reference* 目录」，各技能应有的图片数见上方表格。

## 用法示例

> 用「姿势参考」技能：让我上传的角色按「站立・对立式平衡・手扶腰」姿势站在傍晚的城市街头，写实摄影，竖版 3:4。

Agent 会读 `catalog.csv` 找到对应姿势的 `images/…webp`，把它作为姿势参考图连同角色图一起交给生图/生视频模型；多人互动时为每个角色各取一个姿势。

> 组合「人像参考」「服装参考」「姿势参考」：选一位中长发韩式层次发的人像定脸，配一套冬季大衣穿搭和全身回眸站姿，生成雪后街头全身照。

## 版权与内容说明

- **图片与原始数据著作权归原作者ギア（[@giaaibusi](https://x.com/giaaibusi)，[姿势](https://ai-pose-gallery.pages.dev/) / [服装](https://ai-costume-gallery.pages.dev/) / [人像](https://ai-portrait-gallery.pages.dev/)）所有**；中文整理来自 [anhao/ai-pose-gallery-zh](https://github.com/anhao/ai-pose-gallery-zh)。本仓库仅做格式转换（PNG→WebP、缩放）与技能化封装，不主张任何图片权利，**不得用于商业用途**。权利人如有异议请提 Issue，将立即删除。
- `pose-reference-sexy/couple/all`、`costume-reference-sexy` 及 `pose-reference-upper` 的部分分类含成人向内容（18+）；人像均为 AI 生成的写实人像，请勿用于冒充真实人物，仅供成年人用于艺术创作与动作参考，严禁用于涉及未成年人或任何违法内容。
- 详见 [NOTICE](NOTICE)。
