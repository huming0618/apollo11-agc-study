# 阿波罗 11 号 AGC 研究仓库

本仓库把 **阿波罗 11 号制导计算机（AGC）** 相关的学习指南、资料索引，以及上游飞行软件 / 工具以 submodule 形式集中在一处，方便阅读源码与上手仿真。

> 本仓库**不声称**拥有 NASA / MIT 飞行软件或 Virtual AGC 工具的版权。详见 [NOTICE](NOTICE)。

## 本仓库包含什么

| 路径 | 内容 |
|------|------|
| [`flight-software/Apollo-11`](flight-software/Apollo-11) | 阿波罗 11 飞行软件转写（**Luminary099** 登月舱 + **Comanche055** 指令舱） |
| [`tools/virtualagc`](tools/virtualagc) | Virtual AGC：汇编器、仿真器、Docker 等完整工具链 |
| [`tools/webAGC`](tools/webAGC) | 浏览器端 Wasm AGC + DSKY 演示 |
| [`docs/`](docs/) | 中文资料清单、中/英文运行指南 |

## 快速链接

- **飞行软件（推荐从这里读）**
  - 登月舱 LM：[`flight-software/Apollo-11/Luminary099`](flight-software/Apollo-11/Luminary099)（Luminary 1A / LMY99）
  - 指令舱 CM：[`flight-software/Apollo-11/Comanche055`](flight-software/Apollo-11/Comanche055)（Colossus 2A / Comanche 055）
- **工具**
  - Virtual AGC：[`tools/virtualagc`](tools/virtualagc)
  - webAGC：[`tools/webAGC`](tools/webAGC)
- **文档**
  - 资料清单（中文）：[`docs/sources-zh.md`](docs/sources-zh.md)
  - 运行指南（中文）：[`docs/howto-zh.md`](docs/howto-zh.md)
  - 运行指南（英文）：[`docs/howto-en.md`](docs/howto-en.md)

## 快速开始

1. **最快**：打开在线演示  
   **https://michaelfranzl.github.io/webAGC/demo/**  
   加载 `Luminary099.bin` 或 `Comanche055.bin`，再点 **Run**。  
   灯测：`VERB 35 ENTR`；显示运行时间：`VERB 16 NOUN 65 ENTR`。

2. **本地 / Docker**：见 [`docs/howto-zh.md`](docs/howto-zh.md)（webAGC 本地、Docker VirtualAGC、原生 `make` 摘要）。

3. **读源码**：从 [`docs/sources-zh.md`](docs/sources-zh.md) 的「建议先读文件」开始。

## 带 submodule 克隆

```bash
git clone --recurse-submodules https://github.com/huming0618/apollo11-agc-study.git
```

若已克隆但未拉 submodule：

```bash
git submodule update --init --depth 1
```

## 上游归属

| 项目 | 说明 |
|------|------|
| [Virtual AGC](http://www.ibiblio.org/apollo/) | 数字化、工具链与权威文档门户（Ron Burkey 等） |
| [chrislgarry/Apollo-11](https://github.com/chrislgarry/Apollo-11) | 阿波罗 11 源码 GitHub 转写；**Public Domain Mark 1.0** |
| [virtualagc/virtualagc](https://github.com/virtualagc/virtualagc) | 工具多为 **GPL-2.0+**；其中飞行 AGC/AGS 软件视为公有领域 |
| [michaelfranzl/webAGC](https://github.com/michaelfranzl/webAGC) | 浏览器 Wasm 演示（见其 LICENSE） |

扫描件来源示例：  
[Luminary 099 扫描](http://www.ibiblio.org/apollo/ScansForConversion/Luminary099/) ·  
[Comanche 055 扫描](http://www.ibiblio.org/apollo/ScansForConversion/Comanche055/)

## 许可说明

见根目录 [NOTICE](NOTICE)。文档为本仓库学习笔记；飞行软件公有领域标记以上游为准；Virtual AGC 工具遵循 GPL-2.0+。
