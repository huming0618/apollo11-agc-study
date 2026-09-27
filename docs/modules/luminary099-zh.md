# Luminary099 模块表（中文）

登月舱（LM）阿波罗 11 绳存储器：**Luminary 1A / LMY99**。路径均相对本仓库根目录；文件名已在 `flight-software/Apollo-11/Luminary099/` 下核实存在。

目录索引（上游页码 ↔ 文件）：[`flight-software/Apollo-11/Luminary099/README.md`](../../flight-software/Apollo-11/Luminary099/README.md)  
GitHub：https://github.com/huming0618/apollo11-agc-study/tree/main/flight-software/Apollo-11/Luminary099

导读入口：[`../reading-map-zh.md`](../reading-map-zh.md) · [`../walkthroughs/executive-zh.md`](../walkthroughs/executive-zh.md) · [`../walkthroughs/landing-zh.md`](../walkthroughs/landing-zh.md) · [`../walkthroughs/dsky-pinball-zh.md`](../walkthroughs/dsky-pinball-zh.md)

---

## 总装与资料

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `README.md` | 源码分文件索引与页码对照 | `flight-software/Apollo-11/Luminary099/README.md` |
| `MAIN.agc` | 无链接器时代的总装入口（include 全部分块） | `flight-software/Apollo-11/Luminary099/MAIN.agc` |
| `ASSEMBLY_AND_OPERATION_INFORMATION.agc` | 装配/运行信息、log section 表、Verb·Noun 等操作资料 | `flight-software/Apollo-11/Luminary099/ASSEMBLY_AND_OPERATION_INFORMATION.agc` |
| `TAGS_FOR_RELATIVE_SETLOC.agc` | 相对 SETLOC / 银行放置相关标签 | `flight-software/Apollo-11/Luminary099/TAGS_FOR_RELATIVE_SETLOC.agc` |
| `CONTROLLED_CONSTANTS.agc` | 受控常量池 | `flight-software/Apollo-11/Luminary099/CONTROLLED_CONSTANTS.agc` |
| `INPUT_OUTPUT_CHANNEL_BIT_DESCRIPTIONS.agc` | I/O 通道位含义说明 | `flight-software/Apollo-11/Luminary099/INPUT_OUTPUT_CHANNEL_BIT_DESCRIPTIONS.agc` |
| `FLAGWORD_ASSIGNMENTS.agc` | 标志字（flagword）位分配 | `flight-software/Apollo-11/Luminary099/FLAGWORD_ASSIGNMENTS.agc` |
| `ERASABLE_ASSIGNMENTS.agc` | 可擦存储器（RAM）符号与布局 | `flight-software/Apollo-11/Luminary099/ERASABLE_ASSIGNMENTS.agc` |
| `FIXED_FIXED_CONSTANT_POOL.agc` | 固定存储常量池 | `flight-software/Apollo-11/Luminary099/FIXED_FIXED_CONSTANT_POOL.agc` |

---

## 启动、重启与相位

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `FRESH_START_AND_RESTART.agc` | 上电 fresh start 与各类 restart 入口逻辑 | `flight-software/Apollo-11/Luminary099/FRESH_START_AND_RESTART.agc` |
| `RESTART_TABLES.agc` | 重启表数据 | `flight-software/Apollo-11/Luminary099/RESTART_TABLES.agc` |
| `RESTARTS_ROUTINE.agc` | 重启例程实现 | `flight-software/Apollo-11/Luminary099/RESTARTS_ROUTINE.agc` |
| `PHASE_TABLE_MAINTENANCE.agc` | 相位（phase）表维护，支撑可重启任务结构 | `flight-software/Apollo-11/Luminary099/PHASE_TABLE_MAINTENANCE.agc` |
| `ALARM_AND_ABORT.agc` | 程序报警与 abort 相关处理入口 | `flight-software/Apollo-11/Luminary099/ALARM_AND_ABORT.agc` |
| `AGC_BLOCK_TWO_SELF_CHECK.agc` | Block II AGC 自检 | `flight-software/Apollo-11/Luminary099/AGC_BLOCK_TWO_SELF_CHECK.agc` |

---

## 执行体、定时、解释器与中断

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `EXECUTIVE.agc` | 作业（job）调度：NOVAC / FINDVAC、优先级、ENDOFJOB 等 | `flight-software/Apollo-11/Luminary099/EXECUTIVE.agc` |
| `WAITLIST.agc` | 定时等待列表（短周期任务调度） | `flight-software/Apollo-11/Luminary099/WAITLIST.agc` |
| `INTERPRETER.agc` | 解释型指令虚拟机（向量/矩阵等） | `flight-software/Apollo-11/Luminary099/INTERPRETER.agc` |
| `INTERPRETIVE_CONSTANT.agc` | 解释器相关常量 | `flight-software/Apollo-11/Luminary099/INTERPRETIVE_CONSTANT.agc` |
| `INTER-BANK_COMMUNICATION.agc` | 跨银行调用与通信辅助 | `flight-software/Apollo-11/Luminary099/INTER-BANK_COMMUNICATION.agc` |
| `INTERRUPT_LEAD_INS.agc` | 中断向量/入口引导 | `flight-software/Apollo-11/Luminary099/INTERRUPT_LEAD_INS.agc` |
| `T4RUPT_PROGRAM.agc` | T4 周期中断程序（显示、外设等时基） | `flight-software/Apollo-11/Luminary099/T4RUPT_PROGRAM.agc` |
| `T6-RUPT_PROGRAMS.agc` | T6 中断相关程序 | `flight-software/Apollo-11/Luminary099/T6-RUPT_PROGRAMS.agc` |
| `SINGLE_PRECISION_SUBROUTINES.agc` | 单精度辅助子程序 | `flight-software/Apollo-11/Luminary099/SINGLE_PRECISION_SUBROUTINES.agc` |
| `RTB_OP_CODES.agc` | RTB 操作码相关 | `flight-software/Apollo-11/Luminary099/RTB_OP_CODES.agc` |

---

## DSKY / Pinball（人机界面）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `PINBALL_GAME_BUTTONS_AND_LIGHTS.agc` | 「弹球」键盘与显示主程序（Verb/Noun） | `flight-software/Apollo-11/Luminary099/PINBALL_GAME_BUTTONS_AND_LIGHTS.agc` |
| `PINBALL_NOUN_TABLES.agc` | Noun 表与显示/装载格式 | `flight-software/Apollo-11/Luminary099/PINBALL_NOUN_TABLES.agc` |
| `EXTENDED_VERBS.agc` | 扩展动词（超出 Pinball 核心的 Verb） | `flight-software/Apollo-11/Luminary099/EXTENDED_VERBS.agc` |
| `KEYRUPT_UPRUPT.agc` | 键盘中断与上行（uplink）中断入口 | `flight-software/Apollo-11/Luminary099/KEYRUPT_UPRUPT.agc` |
| `DISPLAY_INTERFACE_ROUTINES.agc` | 显示接口例程（程序侧请求 DSKY） | `flight-software/Apollo-11/Luminary099/DISPLAY_INTERFACE_ROUTINES.agc` |

精读入口：[`../walkthroughs/dsky-pinball-zh.md`](../walkthroughs/dsky-pinball-zh.md)

---

## 月球着陆与动力飞行

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `THE_LUNAR_LANDING.agc` | 着陆流程编排（含 P63 制动段等入口） | `flight-software/Apollo-11/Luminary099/THE_LUNAR_LANDING.agc` |
| `LUNAR_LANDING_GUIDANCE_EQUATIONS.agc` | 着陆制导方程 | `flight-software/Apollo-11/Luminary099/LUNAR_LANDING_GUIDANCE_EQUATIONS.agc` |
| `THROTTLE_CONTROL_ROUTINES.agc` | 主发动机油门控制 | `flight-software/Apollo-11/Luminary099/THROTTLE_CONTROL_ROUTINES.agc` |
| `P70-P71.agc` | 着陆中止程序 P70/P71 | `flight-software/Apollo-11/Luminary099/P70-P71.agc` |
| `BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc` | 主点火编排（Burn Baby Burn） | `flight-software/Apollo-11/Luminary099/BURN_BABY_BURN--MASTER_IGNITION_ROUTINE.agc` |
| `SERVICER.agc` | 导航/服务循环重要部分（平均 G 等） | `flight-software/Apollo-11/Luminary099/SERVICER.agc` |
| `FINDCDUW--GUIDAP_INTERFACE.agc` | 制导与数字自动驾驶接口（CDUW） | `flight-software/Apollo-11/Luminary099/FINDCDUW--GUIDAP_INTERFACE.agc` |
| `LANDING_ANALOG_DISPLAYS.agc` | 着陆相关模拟量显示 | `flight-software/Apollo-11/Luminary099/LANDING_ANALOG_DISPLAYS.agc` |
| `ASCENT_GUIDANCE.agc` | 上升段制导 | `flight-software/Apollo-11/Luminary099/ASCENT_GUIDANCE.agc` |
| `P12.agc` | 动力上升相关程序 P12 | `flight-software/Apollo-11/Luminary099/P12.agc` |
| `POWERED_FLIGHT_SUBROUTINES.agc` | 动力飞行通用子程序 | `flight-software/Apollo-11/Luminary099/POWERED_FLIGHT_SUBROUTINES.agc` |

精读入口：[`../walkthroughs/landing-zh.md`](../walkthroughs/landing-zh.md)

---

## 主要任务程序（P 系列摘选）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `P20-P25.agc` | 交会雷达跟踪等 P20–P25 | `flight-software/Apollo-11/Luminary099/P20-P25.agc` |
| `P30_P37.agc` | 外推/机动准备类 P30 族等 | `flight-software/Apollo-11/Luminary099/P30_P37.agc` |
| `P32-P35_P72-P75.agc` | CSI/CDH 等交会机动相关 | `flight-software/Apollo-11/Luminary099/P32-P35_P72-P75.agc` |
| `P34-35_P74-75.agc` | TPI/TPM 等交会相关 | `flight-software/Apollo-11/Luminary099/P34-35_P74-75.agc` |
| `P40-P47.agc` | 动力机动 / DPS·APS 相关程序族 | `flight-software/Apollo-11/Luminary099/P40-P47.agc` |
| `P51-P53.agc` | IMU 定向/星体相关对准程序 | `flight-software/Apollo-11/Luminary099/P51-P53.agc` |
| `P76.agc` | 目标 ΔV 更新等 | `flight-software/Apollo-11/Luminary099/P76.agc` |
| `GENERAL_LAMBERT_AIMPOINT_GUIDANCE.agc` | Lambert 瞄准点通用制导 | `flight-software/Apollo-11/Luminary099/GENERAL_LAMBERT_AIMPOINT_GUIDANCE.agc` |
| `R30.agc` / `R31.agc` / `R60_62.agc` / `R63.agc` | 例程 R30/R31/R60–62/R63（姿态与显示辅助等） | `flight-software/Apollo-11/Luminary099/` 下同名文件 |

---

## 姿态控制 / DAP（LM）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `DAPIDLER_PROGRAM.agc` | DAP 空闲/调度相关 | `flight-software/Apollo-11/Luminary099/DAPIDLER_PROGRAM.agc` |
| `DAP_INTERFACE_SUBROUTINES.agc` | DAP 接口子程序 | `flight-software/Apollo-11/Luminary099/DAP_INTERFACE_SUBROUTINES.agc` |
| `P-AXIS_RCS_AUTOPILOT.agc` | P 轴 RCS 自动驾驶 | `flight-software/Apollo-11/Luminary099/P-AXIS_RCS_AUTOPILOT.agc` |
| `Q_R-AXIS_RCS_AUTOPILOT.agc` | Q/R 轴 RCS 自动驾驶 | `flight-software/Apollo-11/Luminary099/Q_R-AXIS_RCS_AUTOPILOT.agc` |
| `TJET_LAW.agc` | 喷管点火时间律 | `flight-software/Apollo-11/Luminary099/TJET_LAW.agc` |
| `TRIM_GIMBAL_CONTROL_SYSTEM.agc` | 配平万向架控制 | `flight-software/Apollo-11/Luminary099/TRIM_GIMBAL_CONTROL_SYSTEM.agc` |
| `AOSTASK_AND_AOSJOB.agc` | 角加速度估计任务/作业 | `flight-software/Apollo-11/Luminary099/AOSTASK_AND_AOSJOB.agc` |
| `ATTITUDE_MANEUVER_ROUTINE.agc` | 姿态机动例程 | `flight-software/Apollo-11/Luminary099/ATTITUDE_MANEUVER_ROUTINE.agc` |
| `KALCMANU_STEERING.agc` | KALCMANU 导引 | `flight-software/Apollo-11/Luminary099/KALCMANU_STEERING.agc` |
| `GIMBAL_LOCK_AVOIDANCE.agc` | 万向架锁定回避 | `flight-software/Apollo-11/Luminary099/GIMBAL_LOCK_AVOIDANCE.agc` |
| `RCS_FAILURE_MONITOR.agc` | RCS 故障监视 | `flight-software/Apollo-11/Luminary099/RCS_FAILURE_MONITOR.agc` |
| `SPS_BACK-UP_RCS_CONTROL.agc` | SPS 备份式 RCS 控制相关 | `flight-software/Apollo-11/Luminary099/SPS_BACK-UP_RCS_CONTROL.agc` |
| `KALMAN_FILTER.agc` | 卡尔曼滤波相关片段 | `flight-software/Apollo-11/Luminary099/KALMAN_FILTER.agc` |

---

## 导航、IMU、雷达与几何

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `ORBITAL_INTEGRATION.agc` | 轨道积分 | `flight-software/Apollo-11/Luminary099/ORBITAL_INTEGRATION.agc` |
| `INTEGRATION_INITIALIZATION.agc` | 积分初始化 | `flight-software/Apollo-11/Luminary099/INTEGRATION_INITIALIZATION.agc` |
| `CONIC_SUBROUTINES.agc` | 圆锥曲线子程序 | `flight-software/Apollo-11/Luminary099/CONIC_SUBROUTINES.agc` |
| `MEASUREMENT_INCORPORATION.agc` | 测量并入状态 | `flight-software/Apollo-11/Luminary099/MEASUREMENT_INCORPORATION.agc` |
| `IMU_COMPENSATION_PACKAGE.agc` | IMU 误差补偿 | `flight-software/Apollo-11/Luminary099/IMU_COMPENSATION_PACKAGE.agc` |
| `IMU_MODE_SWITCHING_ROUTINES.agc` | IMU 模式切换 | `flight-software/Apollo-11/Luminary099/IMU_MODE_SWITCHING_ROUTINES.agc` |
| `INFLIGHT_ALIGNMENT_ROUTINES.agc` | 飞行中对准例程 | `flight-software/Apollo-11/Luminary099/INFLIGHT_ALIGNMENT_ROUTINES.agc` |
| `AOTMARK.agc` | 光学瞄准镜（AOT）打标 | `flight-software/Apollo-11/Luminary099/AOTMARK.agc` |
| `RADAR_LEADIN_ROUTINES.agc` | 雷达引导例程 | `flight-software/Apollo-11/Luminary099/RADAR_LEADIN_ROUTINES.agc` |
| `LEM_GEOMETRY.agc` | LM 几何变换 | `flight-software/Apollo-11/Luminary099/LEM_GEOMETRY.agc` |
| `LATITUDE_LONGITUDE_SUBROUTINES.agc` | 经纬度子程序 | `flight-software/Apollo-11/Luminary099/LATITUDE_LONGITUDE_SUBROUTINES.agc` |
| `PLANETARY_INERTIAL_ORIENTATION.agc` | 行星惯性方位 | `flight-software/Apollo-11/Luminary099/PLANETARY_INERTIAL_ORIENTATION.agc` |
| `LUNAR_AND_SOLAR_EPHEMERIDES_SUBROUTINES.agc` | 月/日星历子程序 | `flight-software/Apollo-11/Luminary099/LUNAR_AND_SOLAR_EPHEMERIDES_SUBROUTINES.agc` |
| `TIME_OF_FREE_FALL.agc` | 自由落体时间相关 | `flight-software/Apollo-11/Luminary099/TIME_OF_FREE_FALL.agc` |
| `GROUND_TRACKING_DETERMINATION_PROGRAM.agc` | 地面轨迹确定 | `flight-software/Apollo-11/Luminary099/GROUND_TRACKING_DETERMINATION_PROGRAM.agc` |
| `STABLE_ORBIT.agc` | 稳定轨道相关 | `flight-software/Apollo-11/Luminary099/STABLE_ORBIT.agc` |

---

## 遥测、服务与其它

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `DOWN_TELEMETRY_PROGRAM.agc` | 下行遥测程序 | `flight-software/Apollo-11/Luminary099/DOWN_TELEMETRY_PROGRAM.agc` |
| `DOWNLINK_LISTS.agc` | 下行列表定义 | `flight-software/Apollo-11/Luminary099/DOWNLINK_LISTS.agc` |
| `UPDATE_PROGRAM.agc` | 上行更新程序 | `flight-software/Apollo-11/Luminary099/UPDATE_PROGRAM.agc` |
| `SERVICE_ROUTINES.agc` | 通用服务例程（含部分模式切换辅助） | `flight-software/Apollo-11/Luminary099/SERVICE_ROUTINES.agc` |
| `AGS_INITIALIZATION.agc` | 中止制导系统（AGS）初始化相关 | `flight-software/Apollo-11/Luminary099/AGS_INITIALIZATION.agc` |
| `S-BAND_ANTENNA_FOR_LM.agc` | LM S 波段天线指向 | `flight-software/Apollo-11/Luminary099/S-BAND_ANTENNA_FOR_LM.agc` |
| `SYSTEM_TEST_STANDARD_LEAD_INS.agc` | 系统测试标准入口 | `flight-software/Apollo-11/Luminary099/SYSTEM_TEST_STANDARD_LEAD_INS.agc` |
| `IMU_PERFORMANCE_TEST_2.agc` / `IMU_PERFORMANCE_TESTS_4.agc` | IMU 性能测试 | `flight-software/Apollo-11/Luminary099/` 下同名文件 |

---

## 说明

- 完整文件列表以目录 `ls` 与上游 `README.md` 为准；上表按学习优先级归类，**不是**汇编顺序的唯一权威。
- 未改动任何 submodule 内 `.agc`；本页仅为中文索引。
- GitHub 单文件 URL 形式：`https://github.com/huming0618/apollo11-agc-study/blob/main/flight-software/Apollo-11/Luminary099/<文件名>`
