# 阅读地图（中文导读入口）

本文给出阿波罗 11 号 AGC 源码的**建议学习路径**：入门 → OS（执行体 / 调度）→ 着陆（LM）→ 指令舱（CM）。路径均相对本仓库根目录；并附 GitHub web URL（`main` 分支）。

> 本页只做导航与阅读顺序，不修改 submodule 内 `.agc`。命令与仿真步骤见 [`howto-zh.md`](howto-zh.md)；版本与来源见 [`sources-zh.md`](sources-zh.md)。

---

## 0. 先弄清两套绳存储器

| 航天器 | 目录 | 说明 |
|--------|------|------|
| 登月舱 LM | [`flight-software/Apollo-11/Luminary099`](../flight-software/Apollo-11/Luminary099) | Luminary 1A / LMY99 |
| 指令舱 CM | [`flight-software/Apollo-11/Comanche055`](../flight-software/Apollo-11/Comanche055) | Colossus 2A / Comanche 055 |

GitHub：

- https://github.com/huming0618/apollo11-agc-study/tree/main/flight-software/Apollo-11/Luminary099
- https://github.com/huming0618/apollo11-agc-study/tree/main/flight-software/Apollo-11/Comanche055

---

## 1. 入门（先建立「从哪打开、怎么对照」）

建议顺序：

1. 本仓库总览：[`README.md`](../README.md)  
   https://github.com/huming0618/apollo11-agc-study/blob/main/README.md
2. 资料与版本：[`docs/sources-zh.md`](sources-zh.md)  
   https://github.com/huming0618/apollo11-agc-study/blob/main/docs/sources-zh.md
3. 跑起来（可选但强烈推荐）：[`docs/howto-zh.md`](howto-zh.md)  
   https://github.com/huming0618/apollo11-agc-study/blob/main/docs/howto-zh.md
4. LM 目录索引：[`flight-software/Apollo-11/Luminary099/README.md`](../flight-software/Apollo-11/Luminary099/README.md)  
   https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/README.md
5. 总装入口（无链接器时代的 include 清单）：[`.../Luminary099/MAIN.agc`](../flight-software/Apollo-11/Luminary099/MAIN.agc)  
   https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/MAIN.agc
6. 装配与运行信息 / Verb·Noun 清单入口：[`.../ASSEMBLY_AND_OPERATION_INFORMATION.agc`](../flight-software/Apollo-11/Luminary099/ASSEMBLY_AND_OPERATION_INFORMATION.agc)  
   https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/ASSEMBLY_AND_OPERATION_INFORMATION.agc
7. 模块表（本仓库中文索引）：[`docs/modules/luminary099-zh.md`](modules/luminary099-zh.md) · [`docs/modules/comanche055-zh.md`](modules/comanche055-zh.md)

---

## 2. OS 核心（理解「任务怎么跑起来」）

AGC 没有现代意义上的进程模型，但有明确的 **Executive（作业调度）**、**WAITLIST（定时）**、**Interpreter（解释型运算）** 与 **Fresh Start / Restart**。

建议阅读顺序：

| 顺序 | 相对路径 | GitHub |
|------|----------|--------|
| 1 | [`docs/walkthroughs/executive-zh.md`](walkthroughs/executive-zh.md) | https://github.com/huming0618/apollo11-agc-study/blob/main/docs/walkthroughs/executive-zh.md |
| 2 | [`flight-software/Apollo-11/Luminary099/EXECUTIVE.agc`](../flight-software/Apollo-11/Luminary099/EXECUTIVE.agc) | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/EXECUTIVE.agc |
| 3 | [`.../WAITLIST.agc`](../flight-software/Apollo-11/Luminary099/WAITLIST.agc) | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/WAITLIST.agc |
| 4 | [`.../FRESH_START_AND_RESTART.agc`](../flight-software/Apollo-11/Luminary099/FRESH_START_AND_RESTART.agc) | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/FRESH_START_AND_RESTART.agc |
| 5 | [`.../ERASABLE_ASSIGNMENTS.agc`](../flight-software/Apollo-11/Luminary099/ERASABLE_ASSIGNMENTS.agc)（RAM 符号） | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/ERASABLE_ASSIGNMENTS.agc |
| 6 | [`.../INTERPRETER.agc`](../flight-software/Apollo-11/Luminary099/INTERPRETER.agc)（可稍后） | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/INTERPRETER.agc |

配套人机界面（常与 OS 并行读）：[`docs/walkthroughs/dsky-pinball-zh.md`](walkthroughs/dsky-pinball-zh.md)。

CM 侧同名核心文件在 `Comanche055/` 下（如 `EXECUTIVE.agc`、`WAITLIST.agc`），概念相通，细节以各自文件为准。

---

## 3. 着陆（LM / Luminary099）

月球着陆是 Luminary 最有故事性的一条线：编排 → 制导方程 → 油门 → 中止。

| 顺序 | 相对路径 | GitHub |
|------|----------|--------|
| 1 | [`docs/walkthroughs/landing-zh.md`](walkthroughs/landing-zh.md) | https://github.com/huming0618/apollo11-agc-study/blob/main/docs/walkthroughs/landing-zh.md |
| 2 | [`.../THE_LUNAR_LANDING.agc`](../flight-software/Apollo-11/Luminary099/THE_LUNAR_LANDING.agc) | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/THE_LUNAR_LANDING.agc |
| 3 | [`.../LUNAR_LANDING_GUIDANCE_EQUATIONS.agc`](../flight-software/Apollo-11/Luminary099/LUNAR_LANDING_GUIDANCE_EQUATIONS.agc) | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/LUNAR_LANDING_GUIDANCE_EQUATIONS.agc |
| 4 | [`.../THROTTLE_CONTROL_ROUTINES.agc`](../flight-software/Apollo-11/Luminary099/THROTTLE_CONTROL_ROUTINES.agc) | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/THROTTLE_CONTROL_ROUTINES.agc |
| 5 | [`.../P70-P71.agc`](../flight-software/Apollo-11/Luminary099/P70-P71.agc)（着陆中止） | https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/P70-P71.agc |
| 6 | 相关：[`SERVICER.agc`](../flight-software/Apollo-11/Luminary099/SERVICER.agc)、[`BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc`](../flight-software/Apollo-11/Luminary099/BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc)、[`ALARM_AND_ABORT.agc`](../flight-software/Apollo-11/Luminary099/ALARM_AND_ABORT.agc) | 同目录下对应 blob URL |

---

## 4. 指令舱（CM / Comanche055）

在掌握 Executive + Pinball 之后，再读 CM 特有部分（再入、TVC、RCS-CSM 等）。

建议：

1. [`flight-software/Apollo-11/Comanche055/README.md`](../flight-software/Apollo-11/Comanche055/README.md)  
   https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Comanche055/README.md
2. 模块表：[`docs/modules/comanche055-zh.md`](modules/comanche055-zh.md)
3. [`.../MAIN.agc`](../flight-software/Apollo-11/Comanche055/MAIN.agc) → [`ASSEMBLY_AND_OPERATION_INFORMATION.agc`](../flight-software/Apollo-11/Comanche055/ASSEMBLY_AND_OPERATION_INFORMATION.agc) → [`FRESH_START_AND_RESTART.agc`](../flight-software/Apollo-11/Comanche055/FRESH_START_AND_RESTART.agc)
4. 再入主链：[`REENTRY_CONTROL.agc`](../flight-software/Apollo-11/Comanche055/REENTRY_CONTROL.agc)、[`P61-P67.agc`](../flight-software/Apollo-11/Comanche055/P61-P67.agc)、[`CM_ENTRY_DIGITAL_AUTOPILOT.agc`](../flight-software/Apollo-11/Comanche055/CM_ENTRY_DIGITAL_AUTOPILOT.agc)
5. 推力矢量控制：[`TVCINITIALIZE.agc`](../flight-software/Apollo-11/Comanche055/TVCINITIALIZE.agc)、[`TVCEXECUTIVE.agc`](../flight-software/Apollo-11/Comanche055/TVCEXECUTIVE.agc)、[`TVCDAPS.agc`](../flight-software/Apollo-11/Comanche055/TVCDAPS.agc)

GitHub 树：https://github.com/huming0618/apollo11-agc-study/tree/main/flight-software/Apollo-11/Comanche055

---

## 5. 本仓库中文入口一览

| 文档 | 用途 |
|------|------|
| [`docs/reading-map-zh.md`](reading-map-zh.md) | 本页：学习路径 |
| [`docs/sources-zh.md`](sources-zh.md) | 资料与版本清单 |
| [`docs/howto-zh.md`](howto-zh.md) | 运行 / 仿真指南 |
| [`docs/modules/luminary099-zh.md`](modules/luminary099-zh.md) | LM 模块表 |
| [`docs/modules/comanche055-zh.md`](modules/comanche055-zh.md) | CM 模块表 |
| [`docs/walkthroughs/executive-zh.md`](walkthroughs/executive-zh.md) | Executive 精读入口 |
| [`docs/walkthroughs/landing-zh.md`](walkthroughs/landing-zh.md) | 着陆精读入口 |
| [`docs/walkthroughs/dsky-pinball-zh.md`](walkthroughs/dsky-pinball-zh.md) | DSKY / Pinball 入口 |

---

## 6. 阅读习惯建议

- **先相对路径、再 GitHub**：本地 submodule 拉齐后直接打开 `.agc`；网页浏览用上表 URL。
- **对照扫描件**：ibiblio 扫描见 [`sources-zh.md`](sources-zh.md)；转写与印刷页并非一一「现代 diff」。
- **不要臆造 Verb / 程序步骤**：以 `ASSEMBLY_AND_OPERATION_INFORMATION.agc`、[`howto-zh.md`](howto-zh.md) 与上游已核实内容为准。
- **本仓库文档是导读**：飞行软件版权与归属见根目录 [`NOTICE`](../NOTICE)。
