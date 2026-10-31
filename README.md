# 人生交易所 · 人生K线 — 批量生产规范（Life K-Line Production Playbook）

把一位历史人物的一生，画成一根 K 线：进士及第是涨停，贬谪流放是跌停，退隐善终是横盘退市。本仓库是短视频栏目**「人生K线」**（母品牌**「人生交易所」**）的批量生产规范，供执行 agent 参照生产同规格成片。

规范源头：`life-kline-production` skill（本地生产环境沉淀，含 v1–v8 全部事故教训固化）。
版本日期：**2026-10-24**。

## 怎么用（给 agent 的第一条指令）

> **动手前，先把 [SKILL.md](SKILL.md) 全文读完，再开始任何一步。** 流水线顺序不可乱，硬规则（事故清单）不可跳过，验收门禁未逐项打勾不许交付。

配套必读：

- 文案动笔前读 [narrative-narration/SKILL.md](narrative-narration/SKILL.md)（解说文案方法论：五步工作流 + 输出契约）。
- 录音与质检执行 [docs/audio-qc-standard.md](docs/audio-qc-standard.md)（音频生产质检标准：稿前审 → 分段生成 → 四道门禁）。
- 人物数据按 [templates/figure-template.json](templates/figure-template.json) 起稿，并用 [templates/schema.json](templates/schema.json) 做 jsonschema 校验。
- 发布文案按 [templates/release-copy-template.md](templates/release-copy-template.md) 生成各平台标题/文案/标签。

## 八步流水线概览

| 步 | 内容 | 要点 |
|---|---|---|
| 0 | 立项与价格路径 | 先画价格路径再写文案：一生切 12–18 段，每段定价格起止与形态（涨/跌/横盘/地板/停牌…），标出全片最高/最低价（片头钩子卡用） |
| 1 | 文案 | 按 narrative-narration 契约产出；**因果全覆盖**（每个大涨大跌必有解说句讲清原因）、**转折必落典故**（每节点一张上屏典故卡）、按分句组织（将来逐句对锚） |
| 2 | 录音（音频先行） | 逐段/逐短句合成，**每段录完立即 ASR 转写核对**，不合格只重录该段；解说零加速 |
| 3 | 时间轴与混音 | **解说驱动时间轴**（块时长 = 录音原始时长）；BGM 按块边界编排；混音必须**两段式**（先拼人声成文件，再以文件为输入走 sidechain 闪避），loudnorm 对齐实测约 −17 LUFS / TP −1.5 |
| 4 | 词级锚定 | faster-whisper 词级时刻实测，逐分句建总锚表；大字卡/价格主转折/印章/典故卡/地点标注/finale 元素各自锚到对应分句或关键词时刻 |
| 5 | 数据落盘与渲染 | 人物 JSON 过 schema 校验后渲染；渲染期间数据冻结；渲染前核对全片实际极值与钩子卡数字一致 |
| 6 | 全量审计 | 探针输出与词锚表**逐行**比对偏差（禁止抽查代替）：画面先行 ≤0.5s、其余 ≤0.4s 或落在词内；超标与结构性残余逐行登记，不许隐瞒 |
| 7 | 合成与终验 | **只认交付文件本体**：逐窗转写全窗核对 + verify_audio + 锚点抽帧目检，全过才算完成 |
| 8 | 发布规格 | 发布版一律 1080×1920 母版；**定版默认全片 1.5 倍速**（对已终验成片均匀变速，倍速后复验）；封面用代表作典故画作（公有领域底图 + 程序化原创金线层）；背景地图用**实时位置模型**（staySpans：红点呼吸闪烁当前所在地）；片尾落版「人生交易所 出品」 |

## 目录说明

```
.
├── README.md                        # 本文件：项目说明与使用入口
├── SKILL.md                         # 生产规范主文档（八步流水线 + 十条事故硬规则 + 验收门禁 + 数据契约速查）
├── narrative-narration/
│   └── SKILL.md                     # 解说文案方法论（源：开源 NarratoAI 方法论 + OpenMontage 原则转述）
├── templates/
│   ├── figure-template.json         # 人物数据模板（新人物从此起稿）
│   ├── schema.json                  # 人物数据契约（jsonschema 校验用）
│   └── release-copy-template.md     # 发布文案模板（各平台标题/文案/标签填空式）
└── docs/
    └── audio-qc-standard.md         # 音频生产质检标准（稿前审/分段生成/四道门禁全文）
```

## 品牌口径（发布时遵守）

- 母品牌「**人生交易所**」，王牌栏目「**人生K线**」；合集名统一「人生交易所 · 人生K线」。
- 片尾 OUTRO 落版小字：「人生交易所 出品」。
- 选题走文人线；封面只用公有领域/C
...[truncated 103 chars]
---

📚 **作品目录**：已定版 21 支的完整清单（人物 / 文案 / 封面 / 地点轨迹）见 [WORKS.md](WORKS.md)，选题路线图见 [TODO.md](TODO.md)。
