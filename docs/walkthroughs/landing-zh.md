# 着陆精读入口（Luminary099）

目标：沿「编排 → 制导 → 油门 → 中止」读懂登月舱着陆软件主链。所有路径相对本仓库根目录；**不修改** submodule 内源码。

阅读地图：[`../reading-map-zh.md`](../reading-map-zh.md) · 模块表：[`../modules/luminary099-zh.md`](../modules/luminary099-zh.md)

---

## 建议阅读顺序

| 步 | 文件 | 相对路径 | GitHub |
|----|------|----------|--------|
| 1 | 着陆编排 | `flight-software/Apollo-11/Luminary099/THE_LUNAR_LANDING.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/THE_LUNAR_LANDING.agc |
| 2 | 制导方程 | `flight-software/Apollo-11/Luminary099/LUNAR_LANDING_GUIDANCE_EQUATIONS.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/LUNAR_LANDING_GUIDANCE_EQUATIONS.agc |
| 3 | 油门 | `flight-software/Apollo-11/Luminary099/THROTTLE_CONTROL_ROUTINES.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/THROTTLE_CONTROL_ROUTINES.agc |
| 4 | 中止 P70/P71 | `flight-software/Apollo-11/Luminary099/P70-P71.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/P70-P71.agc |

强烈建议同时打开的支撑文件：

- [`SERVICER.agc`](https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/SERVICER.agc) — 导航/服务循环，着陆过程中持续更新状态  
- [`BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc`](https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc) — 主点火编排（`THE_LUNAR_LANDING` 里会为 Burn Baby Burn 准备 `WHICH` 等）  
- [`FINDCDUW--GUIDAP_INTERFACE.agc`](https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/FINDCDUW--GUIDAP_INTERFACE.agc) — 制导与 DAP 接口  
- [`ALARM_AND_ABORT.agc`](https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/ALARM_AND_ABORT.agc) — 程序报警与 abort 基础设施  
- [`LANDING_ANALOG_DISPLAYS.agc`](https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/LANDING_ANALOG_DISPLAYS.agc) — 着陆模拟显示

---

## 导读

**1. 从 `THE_LUNAR_LANDING.agc` 进入。**  
文件头部标明这是 Luminary 1A build 099 的着陆相关分块。正文很快出现 **P63** 注释标题：月球着陆的**制动段（braking phase）**入口标签为 `P63LM`。阅读时注意它如何做 IMU 状态检查（如 `R02BOTH`）、如何把 `WHICH` 初始化给 Burn Baby Burn、如何清/置一批 flag（源码中有一段「flag orgy」式的 interpretive 清旗），以及如何把着陆点与时间参数送进后续 `GUIDINIT` / 状态外推。同一文件后部还有与更晚阶段相关的 count/标签（例如与 P65/P67 计数相关的 section）；先建立「P63 启动制动着陆」再顺藤摸瓜，不要一次啃完所有阶段。

**2. 再读 `LUNAR_LANDING_GUIDANCE_EQUATIONS.agc`。**  
这是制导方程本体：把当前状态与目标（着陆点、时间、约束）变成制导命令。阅读策略是：找清「每制导周期输入/输出是什么」，以及它如何与 `SERVICER`、姿态接口（`FINDCDUW…`）衔接。把方程文件当成「大脑」，把 `THE_LUNAR_LANDING` 当成「剧本」。

**3. 然后读 `THROTTLE_CONTROL_ROUTINES.agc`。**  
油门例程把制导需求落成主发动机推力命令。结合 flag（例如着陆编排里出现的油门相关旗位名）理解「何时允许自动油门、何时保持」。不要跳过与 servicer / 点火编排的交叉引用。

**4. 最后读 `P70-P71.agc`（着陆中止）。**  
中止程序是着陆链的安全出口：在无法继续着陆时切到中止制导/上升相关路径。对照 `THE_LUNAR_LANDING` 中与 abort 相关的符号引用（如源码中出现的 `LETABORT` 等标签名），看编排层如何把控制交给 P70/P71。报警基础设施仍在 `ALARM_AND_ABORT.agc`——那是更底层的报警/中止服务，与任务级 P70/P71 分工不同。

---

## 阅读提示

- 先读标签与注释中的 **P63 / 阶段名**，再跟 `BANKCALL` / `TC` / interpretive `STCALL` 调用，避免一上来沉浸在矩阵运算里。
- 相位与可重启性：着陆是长任务，常与 `PHASCHNG`、`RESTART_TABLES` 交织；若看到 phase 相关调用，可回到 [`PHASE_TABLE_MAINTENANCE.agc`](https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/PHASE_TABLE_MAINTENANCE.agc) 与 [`../walkthroughs/executive-zh.md`](executive-zh.md)。
- 不臆造行号；印刷页码以各文件头 `Pages:` 注释为准。
- 仿真操作仍以 [`../howto-zh.md`](../howto-zh.md) 为准，本页只做源码导航。
