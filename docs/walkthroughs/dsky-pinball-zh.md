# DSKY / Pinball 精读入口

目标：弄清宇航员如何通过 **DSKY**（Display & Keyboard）与 AGC 对话，以及源码里被称为 **Pinball** 的键盘显示程序如何工作。LM（Luminary099）与 CM（Comanche055）都有同名主文件；下文以 LM 为主并给出 CM 路径。

阅读地图：[`../reading-map-zh.md`](../reading-map-zh.md)

---

## 先读什么

| 顺序 | 内容 | 相对路径 | GitHub |
|------|------|----------|--------|
| 1 | Pinball 主程序 | `flight-software/Apollo-11/Luminary099/PINBALL_GAME_BUTTONS_AND_LIGHTS.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/PINBALL_GAME_BUTTONS_AND_LIGHTS.agc |
| 2 | Noun 表 | `flight-software/Apollo-11/Luminary099/PINBALL_NOUN_TABLES.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/PINBALL_NOUN_TABLES.agc |
| 3 | 扩展动词 | `flight-software/Apollo-11/Luminary099/EXTENDED_VERBS.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/EXTENDED_VERBS.agc |
| 4 | 键盘/上行中断 | `flight-software/Apollo-11/Luminary099/KEYRUPT_UPRUPT.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/KEYRUPT_UPRUPT.agc |
| 5 | 程序侧显示接口 | `flight-software/Apollo-11/Luminary099/DISPLAY_INTERFACE_ROUTINES.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/DISPLAY_INTERFACE_ROUTINES.agc |
| 6 | Verb/Noun 清单入口 | `flight-software/Apollo-11/Luminary099/ASSEMBLY_AND_OPERATION_INFORMATION.agc` | https://github.com/chrislgarry/Apollo-11/blob/911e5c0283c629c50cb97666f34065e8c07d71a5/Luminary099/ASSEMBLY_AND_OPERATION_INFORMATION.agc |

CM 对照（同名或平行文件）：

- `flight-software/Apollo-11/Comanche055/PINBALL_GAME_BUTTONS_AND_LIGHTS.agc`
- `flight-software/Apollo-11/Comanche055/PINBALL_NOUN_TABLES.agc`
- `flight-software/Apollo-11/Comanche055/EXTENDED_VERBS.agc`
- https://github.com/chrislgarry/Apollo-11/tree/911e5c0283c629c50cb97666f34065e8c07d71a5/Comanche055

上手按键示例见 [`../howto-zh.md`](../howto-zh.md)（如灯测、监视运行时间）；**不要**在未核实来源时发明 Verb 序列。

---

## 导读

**Pinball 是什么。**  
`PINBALL_GAME_BUTTONS_AND_LIGHTS.agc` 文件头部的功能说明写得很清楚：这是在 Executive 控制下运行的**键盘与显示系统程序**，处理 AGC 与操作者之间的信息交换。输入来自键盘、内部程序以及上行（uplink）。与操作者通信的语言是一对称为 **Verb（动词）** 与 **Noun（名词）** 的两位数十进制码：Verb 表示做什么，Noun 表示对什么做（Noun 通常对应一组可擦寄存器）。

**Verb 的分组。**  
同一段源码注释把 Verb 分为：显示（displays）、装载（loads）、监视（monitors，约每秒更新的显示）、特殊功能，以及**扩展动词（extended verbs）**——后者不在 Pinball 核心域内，而在 log section `EXTENDED_VERBS`。完整 Verb/Noun 列表指向 `ASSEMBLY_AND_OPERATION_INFORMATION`。因此精读顺序应是：Pinball 主文件建立机制 → Noun 表看数据格式 → Extended Verbs 看「特殊菜单」→ Assembly 文件当词典。

**按键如何进 CPU。**  
注释说明：每次按键触发中断 **KEYRUPT1**，把 5 位键码放入通道 15；KEYRUPT1 再把键码交给键盘显示程序的 **`CHARIN`**，并 `RESUME`。因此阅读路径是：`KEYRUPT_UPRUPT.agc`（中断入口）→ Pinball 里的 `CHARIN` 及后续解码。内部程序则通过 **`NVSUB`** 调用 Pinball，并在 A 中携带 Verb/Noun 编码（注释给出低 7 位 Noun、其上 7 位 Verb 的约定——以你打开的文件原文为准）。

**与 Executive 的关系。**  
Pinball 头部注释提到：它作为 Executive 作业运行；扩展动词会进入 extended verb fan，并仍处于 Pinball 作业上下文中（注释中写到优先级数与 **NOVAC** 作业属性）。读到这里时，回头看 [`executive-zh.md`](executive-zh.md) 会更有画面感：DSKY 不是「另一个操作系统」，而是跑在 Executive 上的高优先级交互作业。

**程序主动「说话」。**  
宇航员按键只是一半；飞行程序常通过 `DISPLAY_INTERFACE_ROUTINES.agc` 请求显示或装载。精读时区分三条来源：键入、`NVSUB`、显示接口例程——它们最终都汇入 Pinball 的显示缓冲与灯/数码管更新逻辑（与 `T4RUPT_PROGRAM.agc` 的周期刷新亦有关联，可在第二轮阅读时再跟）。

---

## 实践建议

1. 在 webAGC / VirtualAGC 里先做 [`howto-zh.md`](../howto-zh.md) 已给出的 Verb 示例，再回源码搜对应 Verb 分发。  
2. 查某个 Noun 的寄存器布局时，优先 `PINBALL_NOUN_TABLES.agc`，再回 `ERASABLE_ASSIGNMENTS.agc`。  
3. 不臆造行号；以文件内标签（如 `CHARIN`、`NVSUB`）与头部页码注释为索引。  
4. 本仓库只提供中文入口文档，不修改上游 `.agc`。
