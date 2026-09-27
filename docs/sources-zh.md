# 阿波罗 11 号 AGC 资料清单

本文整理阿波罗 11 号制导计算机（AGC）研究用的版本对应关系、分级来源、建议先读文件与注意事项。命令与运行步骤以 [`howto-zh.md`](howto-zh.md) / [`howto-en.md`](howto-en.md) 为准，此处不另行发明操作步骤。

---

## 1. 阿波罗 11 发布 / 版本对应（Release map）

| 航天器 | AGC 程序族 | 本任务具体版本 | 目录名（本仓库 submodule） | 汇编标识（摘自源码头） |
|--------|------------|----------------|----------------------------|------------------------|
| 指令舱 CM | Colossus 2A | **Comanche 055** | `flight-software/Apollo-11/Comanche055` | `Assemble revision 055 of AGC program Comanche by NASA` · `2021113-051` · 1969-04-01 |
| 登月舱 LM | Luminary 1A | **Luminary 099**（LMY99） | `flight-software/Apollo-11/Luminary099` | `Assemble revision 001 of AGC program LMY99 by NASA` · `2021112-061` · 1969-07-14 |

要点：

- 「Comanche055 / Luminary099」是社区与 Virtual AGC 常用的**目录 / 绳存储器版本**称呼；与 Colossus / Luminary 家族名并存。
- Virtual AGC 树内同样有 `Comanche055/`、`Luminary099/`（见 `tools/virtualagc`），内容与 chrislgarry 转写同源脉络。
- 仿真器里选软件时，常见标签为 **LUMINARY 99**（LM）与 **COMANCHE 55**（CM）。webAGC 演示使用 `Luminary099.bin` / `Comanche055.bin`。

权威门户：[http://www.ibiblio.org/apollo/](http://www.ibiblio.org/apollo/)

---

## 2. 分级来源（Tier 1–3）

### Tier 1 — 首选（源码 + 扫描 + 权威工具）

| 来源 | URL | 用途 |
|------|-----|------|
| chrislgarry/Apollo-11 | https://github.com/chrislgarry/Apollo-11 | 阿波罗 11 CM/LM 源码转写；本仓库 submodule：`flight-software/Apollo-11`；Public Domain Mark 1.0 |
| virtualagc/virtualagc | https://github.com/virtualagc/virtualagc | 汇编器 yaYUL、仿真器、Docker、多任务源码树；本仓库 submodule：`tools/virtualagc` |
| Virtual AGC 网站 | http://www.ibiblio.org/apollo/ | 下载、Quick Start、DSKY 动词、文档索引 |
| Luminary 099 扫描件 | http://www.ibiblio.org/apollo/ScansForConversion/Luminary099/ | 印刷清单数字化图像（校对用） |
| Comanche 055 扫描件 | http://www.ibiblio.org/apollo/ScansForConversion/Comanche055/ | 同上（CM） |
| 下载 / 构建总览 | http://www.ibiblio.org/apollo/download.html | Docker / VM / 原生编译说明（以该页为准） |

数字化背景：MIT Museum 印刷本扫描（Paul Fjeld 等），Virtual AGC 项目整理；GitHub 转写目标是与扫描件一致并可被校对。

### Tier 2 — 强力辅助（仿真前端、手册、任务上下文）

| 来源 | URL | 用途 |
|------|-----|------|
| michaelfranzl/webAGC | https://github.com/michaelfranzl/webAGC | 浏览器 Wasm AGC + DSKY；本仓库 submodule：`tools/webAGC` |
| webAGC 在线演示 | https://michaelfranzl.github.io/webAGC/demo/ | 零安装试跑 Luminary099 / Comanche055 |
| NASA 阿波罗 11 任务页 | https://www.nasa.gov/mission_pages/apollo/missions/apollo11.html | 任务背景 |
| MIT Museum | http://web.mit.edu/museum/ | 纸质清单保管方（历史语境） |
| Software Heritage 归档 | https://archive.softwareheritage.org/browse/origin/https://github.com/chrislgarry/Apollo-11/ | 源码长期归档 |

另：Virtual AGC 文档与源码中的注释、`ASSEMBLY_AND_OPERATION_INFORMATION.agc` 等文件本身也是「准手册」。

### Tier 3 — 社区 / 二次解读（需交叉核对）

| 来源 | URL | 用途 / 注意 |
|------|-----|-------------|
| Apollo-11 简体中文 README | https://github.com/chrislgarry/Apollo-11/blob/master/Translations/README.zh_cn.md | 上游中文介绍；非飞行软件正文 |
| DeepWiki 等自动文档 | 例如 deepwiki.com 上对 Apollo-11 的页面 | 便于导航，**不能替代**源码与 ibiblio |
| Orbiter / NASSP 等飞行模拟 | 社区项目 | 完整舱体视觉仿真；**不是**纯 AGC 研究本体 |
| 百科、博客、视频 | 各平台 | 入门故事与 1201/1202 报警科普；细节务必回 Tier 1 核对 |

---

## 3. 建议先读文件

路径均相对于 `flight-software/Apollo-11/`（submodule）。

### 登月舱 Luminary099（优先）

| 文件 | 为什么先读 |
|------|------------|
| `Luminary099/README.md` | 源码索引：文件名 ↔ 原清单页码 |
| `Luminary099/MAIN.agc` | 整包 include 清单；无链接器时代的「总装入口」 |
| `Luminary099/ASSEMBLY_AND_OPERATION_INFORMATION.agc` | 装配与运行信息、版本与结构说明 |
| `Luminary099/FRESH_START_AND_RESTART.agc` | 上电 / 重启逻辑 |
| `Luminary099/PINBALL_GAME_BUTTONS_AND_LIGHTS.agc` | DSKY（「弹球」）按键与灯 |
| `Luminary099/PINBALL_NOUN_TABLES.agc` | Verb/Noun 表 |
| `Luminary099/EXTENDED_VERBS.agc` | 扩展动词 |
| `Luminary099/ALARM_AND_ABORT.agc` | 报警与中止（含著名程序报警相关逻辑入口） |
| `Luminary099/THE_LUNAR_LANDING.agc` | 月球着陆流程编排 |
| `Luminary099/LUNAR_LANDING_GUIDANCE_EQUATIONS.agc` | 着陆制导方程 |
| `Luminary099/SERVICER.agc` | 导航 / 服务循环重要部分 |
| `Luminary099/ERASABLE_ASSIGNMENTS.agc` | 可擦存储器（RAM）符号分配 |

### 指令舱 Comanche055

| 文件 | 为什么先读 |
|------|------------|
| `Comanche055/README.md` | 源码索引与分区说明（COMERASE / COMAID 等） |
| `Comanche055/MAIN.agc` | CM 总装入口 |
| `Comanche055/CONTRACT_AND_APPROVALS.agc` | 合同与签署页（历史文献） |
| `Comanche055/ASSEMBLY_AND_OPERATION_INFORMATION.agc` | 装配与运行信息 |
| `Comanche055/FRESH_START_AND_RESTART.agc` | 上电 / 重启 |
| `Comanche055/ALARM_AND_ABORT.agc` | 报警与中止 |
| `Comanche055/ERASABLE_ASSIGNMENTS.agc` | 可擦存储器分配 |

阅读顺序建议：`README` → `MAIN.agc` → `ASSEMBLY_…` → `FRESH_START_…` / `PINBALL_…` → 再进入着陆或 CM 特有程序。

---

## 4. 注意事项（Caveats）

1. **转写 ≠ 原始介质**  
   GitHub 上的 `.agc` 是对照扫描件的人工转写，目标是可被 yaYUL 汇编；与 GAP 时代打印表（交叉引用等）不完全等同。校对请对照 ibiblio 扫描件。

2. **汇编器差异**  
   历史 YUL / GAP 已不可用；现行转写面向 **yaYUL**（Virtual AGC）。格式与当年略有不同，属已知事实，见各目录 README。

3. **版本名易混**  
   「Luminary 1A」「LMY99」「Luminary 099 / 99」指同一阿波罗 11 LM 绳；「Colossus 2A」「Comanche 055」指同一 CM 绳。其他任务（如后续 Apollo）有不同修订号，勿混用二进制。

4. **仿真范围**  
   webAGC / VirtualAGC 核心是 **AGC + DSKY（及部分外设）**，不是完整 LM/CM 仪表飞行游戏。完整视觉仿真需 Orbiter/NASSP 等（Tier 3）。

5. **许可**  
   飞行软件：上游 Public Domain Mark 1.0。Virtual AGC **工具**：GPL-2.0+。本仓库文档仅为学习笔记。详见根目录 [`NOTICE`](../NOTICE)。

6. **子模块体积**  
   `tools/virtualagc` 即使 shallow 也较大；若网络慢，至少保证 `flight-software/Apollo-11` 可用，工具可稍后 `git submodule update --init tools/virtualagc`。

7. **不要发明 Verb/程序步骤**  
   DSKY 示例与 Docker/`make` 步骤以 [`howto-zh.md`](howto-zh.md) 及 ibiblio / 上游 README 已核实内容为准。

---

## 5. 本仓库路径速查

```
apollo11-agc-study/
├── README.md                 # 中文总览
├── NOTICE                    # 归属与许可声明
├── docs/
│   ├── sources-zh.md         # 本清单
│   ├── howto-zh.md           # 运行指南（中文）
│   └── howto-en.md           # 运行指南（英文，已核实命令）
├── flight-software/
│   └── Apollo-11/            # submodule → chrislgarry/Apollo-11
│       ├── Luminary099/
│       └── Comanche055/
└── tools/
    ├── virtualagc/           # submodule → virtualagc/virtualagc
    └── webAGC/               # submodule → michaelfranzl/webAGC
```
