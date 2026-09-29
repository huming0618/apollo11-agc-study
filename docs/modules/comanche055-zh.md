# Comanche055 模块表（中文）

指令舱（CM）阿波罗 11 绳存储器：**Colossus 2A / Comanche 055**。路径均相对本仓库根目录；文件名已在 `flight-software/Apollo-11/Comanche055/` 下核实存在。

目录索引（上游分区 COMERASE / COMAID / …）：[`flight-software/Apollo-11/Comanche055/README.md`](https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Comanche055/README.md)  
GitHub：https://github.com/chrislgarry/Apollo-11/tree/911e5c0283c629c50cb97666f34065e8c07d71a5/Comanche055

导读入口：[`../reading-map-zh.md`](../reading-map-zh.md) · [`../walkthroughs/executive-zh.md`](../walkthroughs/executive-zh.md) · [`../walkthroughs/dsky-pinball-zh.md`](../walkthroughs/dsky-pinball-zh.md)

> 注意：部分文件名与 Luminary099 **不同**（如 `AGC_BLOCK_TWO_SELF-CHECK.agc` 带连字符、`DOWN-TELEMETRY_PROGRAM.agc`、`INTERPRETIVE_CONSTANTS.agc` 复数）。以下均按 Comanche 实际文件名列出。

---

## 总装与资料（INFORMATION）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `README.md` | 源码分文件索引与分区说明 | `flight-software/Apollo-11/Comanche055/README.md` |
| `MAIN.agc` | CM 总装入口（include 全部分块） | `flight-software/Apollo-11/Comanche055/MAIN.agc` |
| `CONTRACT_AND_APPROVALS.agc` | 合同与签署页（历史文献） | `flight-software/Apollo-11/Comanche055/CONTRACT_AND_APPROVALS.agc` |
| `ASSEMBLY_AND_OPERATION_INFORMATION.agc` | 装配/运行信息与操作资料 | `flight-software/Apollo-11/Comanche055/ASSEMBLY_AND_OPERATION_INFORMATION.agc` |
| `TAGS_FOR_RELATIVE_SETLOC.agc` | 相对 SETLOC / 银行放置标签 | `flight-software/Apollo-11/Comanche055/TAGS_FOR_RELATIVE_SETLOC.agc` |
| `ERASABLE_ASSIGNMENTS.agc` | 可擦存储器（RAM）符号与布局（COMERASE） | `flight-software/Apollo-11/Comanche055/ERASABLE_ASSIGNMENTS.agc` |
| `FIXED_FIXED_CONSTANT_POOL.agc` | 固定存储常量池 | `flight-software/Apollo-11/Comanche055/FIXED_FIXED_CONSTANT_POOL.agc` |
| `STAR_TABLES.agc` | 星表数据 | `flight-software/Apollo-11/Comanche055/STAR_TABLES.agc` |

---

## 启动、重启与相位

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `FRESH_START_AND_RESTART.agc` | 上电与重启逻辑 | `flight-software/Apollo-11/Comanche055/FRESH_START_AND_RESTART.agc` |
| `RESTART_TABLES.agc` | 重启表 | `flight-software/Apollo-11/Comanche055/RESTART_TABLES.agc` |
| `RESTARTS_ROUTINE.agc` | 重启例程 | `flight-software/Apollo-11/Comanche055/RESTARTS_ROUTINE.agc` |
| `PHASE_TABLE_MAINTENANCE.agc` | 相位表维护 | `flight-software/Apollo-11/Comanche055/PHASE_TABLE_MAINTENANCE.agc` |
| `ALARM_AND_ABORT.agc` | 报警与 abort | `flight-software/Apollo-11/Comanche055/ALARM_AND_ABORT.agc` |
| `AGC_BLOCK_TWO_SELF-CHECK.agc` | Block II 自检（注意文件名中的连字符） | `flight-software/Apollo-11/Comanche055/AGC_BLOCK_TWO_SELF-CHECK.agc` |

---

## 执行体、定时、解释器与中断（CHIEFTAN 等）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `EXECUTIVE.agc` | 作业调度（NOVAC / FINDVAC / 优先级） | `flight-software/Apollo-11/Comanche055/EXECUTIVE.agc` |
| `WAITLIST.agc` | 定时等待列表 | `flight-software/Apollo-11/Comanche055/WAITLIST.agc` |
| `INTERPRETER.agc` | 解释型指令虚拟机 | `flight-software/Apollo-11/Comanche055/INTERPRETER.agc` |
| `INTERPRETIVE_CONSTANTS.agc` | 解释器常量（复数 CONSTANTS） | `flight-software/Apollo-11/Comanche055/INTERPRETIVE_CONSTANTS.agc` |
| `INTER-BANK_COMMUNICATION.agc` | 跨银行通信 | `flight-software/Apollo-11/Comanche055/INTER-BANK_COMMUNICATION.agc` |
| `INTERRUPT_LEAD_INS.agc` | 中断入口引导 | `flight-software/Apollo-11/Comanche055/INTERRUPT_LEAD_INS.agc` |
| `T4RUPT_PROGRAM.agc` | T4 周期中断程序 | `flight-software/Apollo-11/Comanche055/T4RUPT_PROGRAM.agc` |
| `SINGLE_PRECISION_SUBROUTINES.agc` | 单精度子程序 | `flight-software/Apollo-11/Comanche055/SINGLE_PRECISION_SUBROUTINES.agc` |
| `RT8_OP_CODES.agc` | RTB/RT8 操作码相关 | `flight-software/Apollo-11/Comanche055/RT8_OP_CODES.agc` |

精读入口（概念以 LM 文件导读为主，CM 同名对照）：[`../walkthroughs/executive-zh.md`](../walkthroughs/executive-zh.md)

---

## DSKY / Pinball（COMAID）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `PINBALL_GAME_BUTTONS_AND_LIGHTS.agc` | 键盘与显示主程序（Verb/Noun） | `flight-software/Apollo-11/Comanche055/PINBALL_GAME_BUTTONS_AND_LIGHTS.agc` |
| `PINBALL_NOUN_TABLES.agc` | Noun 表 | `flight-software/Apollo-11/Comanche055/PINBALL_NOUN_TABLES.agc` |
| `EXTENDED_VERBS.agc` | 扩展动词 | `flight-software/Apollo-11/Comanche055/EXTENDED_VERBS.agc` |
| `KEYRUPT_UPRUPT.agc` | 键盘 / 上行中断 | `flight-software/Apollo-11/Comanche055/KEYRUPT_UPRUPT.agc` |
| `DISPLAY_INTERFACE_ROUTINES.agc` | 显示接口例程 | `flight-software/Apollo-11/Comanche055/DISPLAY_INTERFACE_ROUTINES.agc` |

精读入口：[`../walkthroughs/dsky-pinball-zh.md`](../walkthroughs/dsky-pinball-zh.md)

---

## 再入（Entry）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `P61-P67.agc` | 再入相关主要程序 P61–P67 | `flight-software/Apollo-11/Comanche055/P61-P67.agc` |
| `REENTRY_CONTROL.agc` | 再入控制逻辑 | `flight-software/Apollo-11/Comanche055/REENTRY_CONTROL.agc` |
| `ENTRY_LEXICON.agc` | 再入术语/量定义（lexicon） | `flight-software/Apollo-11/Comanche055/ENTRY_LEXICON.agc` |
| `CM_BODY_ATTITUDE.agc` | CM 体坐标姿态相关 | `flight-software/Apollo-11/Comanche055/CM_BODY_ATTITUDE.agc` |
| `CM_ENTRY_DIGITAL_AUTOPILOT.agc` | CM 再入数字自动驾驶 | `flight-software/Apollo-11/Comanche055/CM_ENTRY_DIGITAL_AUTOPILOT.agc` |
| `SERVICER207.agc` | CM 侧 servicer（平均 G / 导航服务循环） | `flight-software/Apollo-11/Comanche055/SERVICER207.agc` |
| `P37_P70.agc` | 返回/再入准备相关程序族 | `flight-software/Apollo-11/Comanche055/P37_P70.agc` |

---

## TVC 与 CSM 姿态控制（TVCDAPS）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `TVCINITIALIZE.agc` | 推力矢量控制（TVC）初始化 | `flight-software/Apollo-11/Comanche055/TVCINITIALIZE.agc` |
| `TVCEXECUTIVE.agc` | TVC 执行调度 | `flight-software/Apollo-11/Comanche055/TVCEXECUTIVE.agc` |
| `TVCMASSPROP.agc` | TVC 质量特性 | `flight-software/Apollo-11/Comanche055/TVCMASSPROP.agc` |
| `TVCRESTARTS.agc` | TVC 重启支持 | `flight-software/Apollo-11/Comanche055/TVCRESTARTS.agc` |
| `TVCDAPS.agc` | TVC 数字自动驾驶 | `flight-software/Apollo-11/Comanche055/TVCDAPS.agc` |
| `TVCSTROKETEST.agc` | TVC 行程测试 | `flight-software/Apollo-11/Comanche055/TVCSTROKETEST.agc` |
| `TVCROLLDAP.agc` | TVC 滚转 DAP | `flight-software/Apollo-11/Comanche055/TVCROLLDAP.agc` |
| `RCS-CSM_DIGITAL_AUTOPILOT.agc` | CSM RCS 数字自动驾驶 | `flight-software/Apollo-11/Comanche055/RCS-CSM_DIGITAL_AUTOPILOT.agc` |
| `RCS-CSM_DAP_EXECUTIVE_PROGRAMS.agc` | CSM RCS DAP 执行程序 | `flight-software/Apollo-11/Comanche055/RCS-CSM_DAP_EXECUTIVE_PROGRAMS.agc` |
| `JET_SELECTION_LOGIC.agc` | 喷管选择逻辑 | `flight-software/Apollo-11/Comanche055/JET_SELECTION_LOGIC.agc` |
| `AUTOMATIC_MANEUVERS.agc` | 自动机动 | `flight-software/Apollo-11/Comanche055/AUTOMATIC_MANEUVERS.agc` |
| `MYSUBS.agc` | TVC/DAP 辅助子程序集 | `flight-software/Apollo-11/Comanche055/MYSUBS.agc` |

---

## 主要任务程序（TROUBLE / COMEKISS 摘选）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `P11.agc` | 地球轨道插入后等早期飞行相关 | `flight-software/Apollo-11/Comanche055/P11.agc` |
| `P20-P25.agc` | 交会雷达跟踪等 | `flight-software/Apollo-11/Comanche055/P20-P25.agc` |
| `P30-P37.agc` | 外推/机动准备（注意连字符写法与 LM 的 `P30_P37` 不同） | `flight-software/Apollo-11/Comanche055/P30-P37.agc` |
| `P32-P33_P72-P73.agc` | CSI 等交会机动相关 | `flight-software/Apollo-11/Comanche055/P32-P33_P72-P73.agc` |
| `P34-35_P74-75.agc` | TPI 等交会相关 | `flight-software/Apollo-11/Comanche055/P34-35_P74-75.agc` |
| `P40-P47.agc` | SPS 动力机动等 | `flight-software/Apollo-11/Comanche055/P40-P47.agc` |
| `P51-P53.agc` | IMU 定向/对准 | `flight-software/Apollo-11/Comanche055/P51-P53.agc` |
| `P76.agc` | 目标 ΔV 更新等 | `flight-software/Apollo-11/Comanche055/P76.agc` |
| `TPI_SEARCH.agc` | TPI 搜索 | `flight-software/Apollo-11/Comanche055/TPI_SEARCH.agc` |
| `R30.agc` / `R31.agc` / `R60_62.agc` | 例程 R30/R31/R60–62 | `flight-software/Apollo-11/Comanche055/` 下同名文件 |
| `STABLE_ORBIT.agc` | 稳定轨道相关 | `flight-software/Apollo-11/Comanche055/STABLE_ORBIT.agc` |
| `GROUND_TRACKING_DETERMINATION_PROGRAM.agc` | 地面轨迹确定 | `flight-software/Apollo-11/Comanche055/GROUND_TRACKING_DETERMINATION_PROGRAM.agc` |
| `LUNAR_LANDMARK_SELECTION_FOR_CM.agc` | CM 月球地标选择 | `flight-software/Apollo-11/Comanche055/LUNAR_LANDMARK_SELECTION_FOR_CM.agc` |
| `S-BAND_ANTENNA_FOR_CM.agc` | CM S 波段天线 | `flight-software/Apollo-11/Comanche055/S-BAND_ANTENNA_FOR_CM.agc` |

---

## 导航、IMU、光学与几何（COMAID 等）

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `ORBITAL_INTEGRATION.agc` | 轨道积分 | `flight-software/Apollo-11/Comanche055/ORBITAL_INTEGRATION.agc` |
| `INTEGRATION_INITIALIZATION.agc` | 积分初始化 | `flight-software/Apollo-11/Comanche055/INTEGRATION_INITIALIZATION.agc` |
| `CONIC_SUBROUTINES.agc` | 圆锥曲线子程序 | `flight-software/Apollo-11/Comanche055/CONIC_SUBROUTINES.agc` |
| `MEASUREMENT_INCORPORATION.agc` | 测量并入 | `flight-software/Apollo-11/Comanche055/MEASUREMENT_INCORPORATION.agc` |
| `IMU_COMPENSATION_PACKAGE.agc` | IMU 补偿 | `flight-software/Apollo-11/Comanche055/IMU_COMPENSATION_PACKAGE.agc` |
| `IMU_MODE_SWITCHING_ROUTINES.agc` | IMU 模式切换 | `flight-software/Apollo-11/Comanche055/IMU_MODE_SWITCHING_ROUTINES.agc` |
| `IMU_CALIBRATION_AND_ALIGNMENT.agc` | IMU 标定与对准 | `flight-software/Apollo-11/Comanche055/IMU_CALIBRATION_AND_ALIGNMENT.agc` |
| `INFLIGHT_ALIGNMENT_ROUTINES.agc` | 飞行中对准 | `flight-software/Apollo-11/Comanche055/INFLIGHT_ALIGNMENT_ROUTINES.agc` |
| `SXTMARK.agc` | 六分仪打标（SXTMARK） | `flight-software/Apollo-11/Comanche055/SXTMARK.agc` |
| `CSM_GEOMETRY.agc` | CSM 几何 | `flight-software/Apollo-11/Comanche055/CSM_GEOMETRY.agc` |
| `ANGLFIND.agc` | 角度寻找 / 机动角相关 | `flight-software/Apollo-11/Comanche055/ANGLFIND.agc` |
| `KALCMANU_STEERING.agc` | KALCMANU 导引 | `flight-software/Apollo-11/Comanche055/KALCMANU_STEERING.agc` |
| `GIMBAL_LOCK_AVOIDANCE.agc` | 万向架锁定回避 | `flight-software/Apollo-11/Comanche055/GIMBAL_LOCK_AVOIDANCE.agc` |
| `LATITUDE_LONGITUDE_SUBROUTINES.agc` | 经纬度子程序 | `flight-software/Apollo-11/Comanche055/LATITUDE_LONGITUDE_SUBROUTINES.agc` |
| `PLANETARY_INERTIAL_ORIENTATION.agc` | 行星惯性方位 | `flight-software/Apollo-11/Comanche055/PLANETARY_INERTIAL_ORIENTATION.agc` |
| `LUNAR_AND_SOLAR_EPHEMERIDES_SUBROUTINES.agc` | 月/日星历 | `flight-software/Apollo-11/Comanche055/LUNAR_AND_SOLAR_EPHEMERIDES_SUBROUTINES.agc` |
| `TIME_OF_FREE_FALL.agc` | 自由落体时间 | `flight-software/Apollo-11/Comanche055/TIME_OF_FREE_FALL.agc` |
| `POWERED_FLIGHT_SUBROUTINES.agc` | 动力飞行子程序 | `flight-software/Apollo-11/Comanche055/POWERED_FLIGHT_SUBROUTINES.agc` |

---

## 遥测与服务

| 文件 | 一句话职责 | 相对路径 |
|------|------------|----------|
| `DOWN-TELEMETRY_PROGRAM.agc` | 下行遥测（注意文件名连字符） | `flight-software/Apollo-11/Comanche055/DOWN-TELEMETRY_PROGRAM.agc` |
| `DOWNLINK_LISTS.agc` | 下行列表 | `flight-software/Apollo-11/Comanche055/DOWNLINK_LISTS.agc` |
| `UPDATE_PROGRAM.agc` | 上行更新 | `flight-software/Apollo-11/Comanche055/UPDATE_PROGRAM.agc` |
| `SERVICE_ROUTINES.agc` | 通用服务例程 | `flight-software/Apollo-11/Comanche055/SERVICE_ROUTINES.agc` |
| `SYSTEM_TEST_STANDARD_LEAD_INS.agc` | 系统测试入口 | `flight-software/Apollo-11/Comanche055/SYSTEM_TEST_STANDARD_LEAD_INS.agc` |

---

## 说明

- 完整列表以 `Comanche055/` 目录与上游 `README.md` 分区表为准。
- 未改动任何 submodule 内 `.agc`；本页仅为中文索引。
- GitHub 单文件：`https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Comanche055/<文件名>`
