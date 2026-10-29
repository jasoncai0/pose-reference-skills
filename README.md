# Pose Reference Skills · 姿势参考技能包

把 [ai-pose-gallery-zh](https://github.com/anhao/ai-pose-gallery-zh) 的 1439 张多角度人体姿势白模图打包成 5 个**自包含**的 Agent 技能（Agent Skills / `SKILL.md` 格式）。
每个技能包自带全部参考图（WebP，900×1200），`references/catalog.csv` 用**相对路径**索引，离线可用，不依赖任何外链。

Five self-contained Agent Skills that bundle 1,439 multi-angle pose mannequin images (WebP, 900×1200). Each skill ships its own images; `references/catalog.csv` points to them with paths relative to the skill root.

## 技能列表

| 技能 | 图片数 | 内容 | 体积 |
|-|-:|-|-:|
| [`pose-reference-standard`](skills/pose-reference-standard) | 365 | 全身单人·标准系（站/坐/跪/蹲/趴/扭身等 9 类） | 12 MB |
| [`pose-reference-upper`](skills/pose-reference-upper) | 400 | 上半身单人（可爱/性感/强调系，部分 18+） | 22 MB |
| [`pose-reference-sexy`](skills/pose-reference-sexy) | 399 | 全身单人·性感系（**18+**） | 19 MB |
| [`pose-reference-couple`](skills/pose-reference-couple) | 275 | 双人（**18+**） | 19 MB |
| [`pose-reference-all`](skills/pose-reference-all) | 1439 | 以上全部（含 18+） | 72 MB |

每张图有 5 种视角中的若干个：正面 / 斜侧 / 侧面 / 俯视 / 仰视。

## 目录结构

```
skills/pose-reference-standard/
├── SKILL.md                  # 技能说明 + 用法 + 姿势目录
├── references/catalog.csv    # id,体系,分类,姿势编号,姿势名称,角度,图片(images/<id>.webp)
└── images/<id>.webp          # 白模姿势图（随技能打包）
```

## 安装

Claude Code（任选一个或多个技能）：

```bash
git clone --depth 1 https://github.com/jasoncai0/pose-reference-skills.git
cp -r pose-reference-skills/skills/pose-reference-standard ~/.claude/skills/
```

其他支持 `SKILL.md` 的 Agent 平台：把整个技能目录（含 `images/`）作为技能包上传即可。

## 用法示例

> 用「姿势参考」技能：让我上传的角色按「站立・对立式平衡・手扶腰」姿势站在傍晚的城市街头，写实摄影，竖版 3:4。

Agent 会读 `catalog.csv` 找到对应姿势的 `images/…webp`，把它作为姿势参考图连同角色图一起交给生图/生视频模型；多人互动时为每个角色各取一个姿势。

## 版权与内容说明

- **图片与原始数据著作权归原作者ギア（[@giaaibusi](https://x.com/giaaibusi)，[ai-pose-gallery.pages.dev](https://ai-pose-gallery.pages.dev/)）所有**；中文整理来自 [anhao/ai-pose-gallery-zh](https://github.com/anhao/ai-pose-gallery-zh)。本仓库仅做格式转换（PNG→WebP）与技能化封装，不主张任何图片权利，**不得用于商业用途**。权利人如有异议请提 Issue，将立即删除。
- `sexy`、`couple`、`all` 及 `upper` 的部分分类含成人向姿势（18+），仅供成年人用于艺术创作与动作参考，严禁用于涉及未成年人或任何违法内容。
- 详见 [NOTICE](NOTICE)。
