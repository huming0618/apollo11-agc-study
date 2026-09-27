# Executive 精读入口

目标：读懂 AGC **作业调度器**（Executive）在做什么，再带着问题打开源码。本文以登月舱 **Luminary099** 为主；指令舱 `Comanche055/EXECUTIVE.agc` 概念平行，细节各自对照。

---

## 先读什么

1. 本页（建立词汇：job / VAC / priority）。
2. 源码：[`flight-software/Apollo-11/Luminary099/EXECUTIVE.agc`](../../flight-software/Apollo-11/Luminary099/EXECUTIVE.agc)  
   GitHub：https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/EXECUTIVE.agc
3. 紧接着：同目录 [`WAITLIST.agc`](../../flight-software/Apollo-11/Luminary099/WAITLIST.agc)（定时短任务）与 [`FRESH_START_AND_RESTART.agc`](../../flight-software/Apollo-11/Luminary099/FRESH_START_AND_RESTART.agc)（谁在开机时把系统拉起来）。
4. 需要查 RAM 符号时：[`ERASABLE_ASSIGNMENTS.agc`](../../flight-software/Apollo-11/Luminary099/ERASABLE_ASSIGNMENTS.agc)。
5. CM 对照：[`flight-software/Apollo-11/Comanche055/EXECUTIVE.agc`](../../flight-software/Apollo-11/Comanche055/EXECUTIVE.agc)。

模块总表：[`../modules/luminary099-zh.md`](../modules/luminary099-zh.md)。阅读地图：[`../reading-map-zh.md`](../reading-map-zh.md)。

---

## 关键概念（对照文件开头注释与入口标签）

打开 `EXECUTIVE.agc` 后，文件前部用注释标出了几类**进入作业请求**的入口（名称以源码标签为准，勿依赖本文臆造行号）：

- **Job（作业）**  
  Executive 调度的基本单位。调用方通过入口登记「要跑哪段代码（2CADR）+ 优先级」，由 Executive 在适当时机切换执行。作业结束走 `ENDOFJOB` 一类路径；也可 `JOBSLEEP` / `JOBWAKE` 等待事件后再醒。

- **NOVAC**  
  源码注释写明：进入**不需要 VAC 区**的作业请求。适合较「基本」（basic）的作业。入口附近会设置 `NEWPRIO`、取 2CADR 到 `NEWLOC`，再转入 Executive 所在银行继续处理。

- **FINDVAC / SPVAC**  
  源码注释写明：进入**需要 VAC 区**的作业请求——例如（部分）解释型（interpretive）作业。`FINDVAC2` 一带会在 `VAC1USE`、`VAC2USE`… 中定位可用 VAC；`SPVAC` 则是「优先级已在 `NEWPRIO`、2CADR 由 A/L 传入」的变体（注释要求调用前 `INHINT`）。

- **VAC（Vector Accumulator Area）**  
  可擦存储器中的一块工作区，供需要较多临时向量/解释器状态的作业使用。没有空闲 VAC 时，需要 VAC 的作业不能立刻按「已找到 VAC」路径推进——读 `FINDVAC2` 段时盯住 `VACnUSE` 相关逻辑即可建立直觉。

- **Priority（优先级）**  
  新作业优先级进入 `NEWPRIO`。更高优先级可打断当前作业：源码提供 `CHANG1`（挂起 basic job）、`CHANG2`（挂起 interpretive job；注释指出负的 `LOC` 表示解释型作业）、以及 `PRIOCHNG`（改当前作业优先级）。调度的核心就是：在登记的作业里选合适者运行，并在优先级变化时换岗。

配合记忆：`WAITLIST` 管的是**按时间触发的短回调**；Executive 管的是**可抢占的作业队列**。二者常被上层程序一起用，但文件职责不同。

---

## 阅读时怎么走（2–4 段导读）

**第一遍：只扫入口标签与注释。** 从 `NOVAC`、`FINDVAC`、`SPVAC`、`CHANG1`/`CHANG2`、`JOBSLEEP`/`JOBWAKE`、`PRIOCHNG`、`ENDOFJOB` 建立「API 面」。先不要陷入每个 `CCS` 分支。文件头的 Virtual AGC 元数据会标明该分块在印刷清单中的页码范围，便于对照 ibiblio 扫描。

**第二遍：跟一条「登记作业」路径。** 任选 `NOVAC` 或 `FINDVAC`，跟到切换银行（如 `EXECBANK`）之后的 `NOVAC2` / `FINDVAC2`。问自己三个问题：优先级存在哪？作业入口地址（2CADR）存在哪？需要 VAC 时如何标记「已占用」？

**第三遍：跟一条「换作业 / 结束作业」路径。** 读 `CHANJOB`、`ENDOFJOB`/`ENDJOB1` 相关控制流，理解「当前作业让出」与「选下一个」在同一套 Executive 银行里完成。遇到 `NEWPRIO`、`NEWLOC`、`EXECTEM1` 等符号，回 `ERASABLE_ASSIGNMENTS.agc` 查定义，而不是猜测。

**第四遍（可选）：与 Pinball / 着陆交叉。** DSKY 路径里，Pinball 常作为 **NOVAC 作业**跑（见 Pinball 文件头部功能说明中的 priority / NOVAC 描述）；着陆程序则大量 `BANKCALL` / 相位与重启表。先把 Executive 当「操作系统内核」，再读应用层会轻松很多。

---

## 不要做的事

- 不要改 submodule 里的 `.agc`；笔记写在本仓库 `docs/`。
- 不要在未打开文件时引用具体行号；印刷「Page nnnn」注释可以当索引，但以你本地文件为准。
- Verb/Noun 操作步骤以 [`../howto-zh.md`](../howto-zh.md) 与 `ASSEMBLY_AND_OPERATION_INFORMATION.agc` 为准。
