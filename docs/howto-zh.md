# 如何运行阿波罗 11 号 AGC 软件（据上游文档核实）

对应英文版：[`howto-en.md`](howto-en.md)。下列命令与步骤来自上游，**请勿在此文档之外臆造 AGC 操作**。

已核对来源：

- https://github.com/michaelfranzl/webAGC（README + demo/README）
- 在线演示：https://michaelfranzl.github.io/webAGC/demo/
- https://github.com/virtualagc/virtualagc（README + Docker/README + Docker/DEPLOYMENT.md + Docker/start.sh）
- http://www.ibiblio.org/apollo/download.html
- http://www.ibiblio.org/apollo/index.html（Quick Start / DSKY 动词）

本仓库若已拉取 submodule，本地路径对应：

- `tools/webAGC`
- `tools/virtualagc`

---

## A) webAGC — 浏览器演示（最简单）

### 1. 前置条件

- **系统：** 任意桌面 OS（Windows / macOS / Linux）
- **浏览器：** 支持 WebAssembly 的现代浏览器（Firefox、Chrome、Edge、Safari 等；Virtual AGC 下载页亦提到 Wasm）。托管演示为静态 HTML/JS/WASM。
- **可选（仅本地服务）：** 较新的 Node.js。demo/README 确认过 **v22.22.2**。浏览器对 Wasm/模块需要通过 **HTTP** 访问（不要用 `file://`）。

### 2. 确切步骤 — 托管演示（无需安装）

1. 打开：**https://michaelfranzl.github.io/webAGC/demo/**
2. 在 **“Load program into fixed memory”** 下选择其一：
   - **Luminary099.bin** — 阿波罗 11 登月舱 AGC
   - **Comanche055.bin** — 阿波罗 11 指令舱 AGC
   - （另有 Validation.bin，用于仿真器自检）
3. 在 **CPU manipulation** 下点击 **Run**（或先 Reset 再 Run）。Virtual AGC 的 Wasm 说明：先**加载程序**，再 Run（或 Step 单步）。
4. 使用屏幕上的 **DSKY**：
   - 点击按键，**或**在 **“DSKY key input”** 中输入：
     - 数字 `0`–`9`，`+`，`-`
     - VERB=`v`，NOUN=`n`，CLR=`c`，KEY REL=`k`，ENTR=`e` 或 Enter，RSET=`r`，PRO=`p`

**演示页记载的示例（Luminary099 与 Comanche055 均可）：**

- 灯测：输入 **VERB 3 5 ENTR** → 键 `v` `3` `5` `e`（或点击 VERB、3、5、ENTR）
- 显示启动以来时间（秒、分、时）：**VERB 1 6 NOUN 6 5 ENTR** → `v` `1` `6` `n` `6` `5` `e`

**Validation.bin（演示）：** OPR ERR 闪烁时按 **PRO**；约 38 秒后 PROG 应显示 **77**（成功）。

### 2b. 确切步骤 — 从仓库本地跑演示（可选）

据 [demo/README.md](https://github.com/michaelfranzl/webAGC/blob/master/demo/README.md)：

```sh
git clone --depth=1 https://github.com/michaelfranzl/webAGC
cd webAGC/demo
npm ci
npm run serve-dev
```

若已克隆本研究仓库并初始化 submodule，可改为：

```sh
cd tools/webAGC/demo
npm ci
npm run serve-dev
```

打开终端打印的 URL（例如 `http://localhost:8000`）。然后按上文加载 Luminary099 / Comanche055 并 Run。

构建 + 静态服务（同一 README）：

```sh
npm run build
npm run serve-build
```

### 3. 预期现象

- **AGC 仿真面板：** 时钟分频、指令/秒、Reset / Pause / Step / Run、State。
- **DSKY：** 指示灯 + PROG / VERB / NOUN / R1–R3 风格数码；可点击键盘。
- **V35E 之后：** 灯测（指示灯 / 88 风格数码 — 与 Virtual AGC 主页上的 V35E 同类）。
- **V16N65E 之后：** 寄存器中实时显示程序启动以来的时间。
- 下方有实时**可擦存储器**（八进制）与 I/O 端口开关。

### 4. 常见坑

- **Run 之前忘记**把 `.bin` 载入固定存储器（绳为空/错误）。
- 本地用 `file://.../index.html` 打开 — 现代浏览器对 Wasm/模块需要 HTTP 服务（demo README + Virtual AGC Wasm 说明）。
- Android 上的 Chromium：演示说明文字键入框可能失效（[Chromium bug 118639](https://bugs.chromium.org/p/chromium/issues/detail?id=118639)）；请用屏幕 DSKY 键。
- 期待完整飞船 / 飞行模拟器 — webAGC 仅有 AGC + DSKY + 存储器视图。

### 5. 链接

- 仓库：https://github.com/michaelfranzl/webAGC
- 演示：https://michaelfranzl.github.io/webAGC/demo/
- Demo README：https://github.com/michaelfranzl/webAGC/blob/master/demo/README.md
- 程序文档：https://www.ibiblio.org/apollo/

---

## B) VirtualAGC 本地 — 优先 Docker

官方说明：可用 Docker 部署 Virtual AGC，无需在宿主机装编译依赖。Docker「GUI 亭」通过 VNC 桌面启动 **VirtualAGC**（浏览器里用 noVNC）。除非需要完整原生工具链，否则优先 Docker，而不是本机 `make`。

### 1. 前置条件（来自 Docker/DEPLOYMENT.md）

- **Docker Engine 20.10+** 或 **Docker Desktop**
- **Docker Compose 2.0+**（Desktop 自带）
- 可用内存 **≥ 2 GB**（Desktop：Settings → Resources → Memory；指南建议 **4 GB+**）
- 主机端口 **6080**（noVNC）与 **5900**（VNC）空闲
- **构建镜像**时需能访问 GitHub（Dockerfile 会克隆并编译 VirtualAGC）
- **磁盘：** DEPLOYMENT 建议构建预留 **≥ ~5 GB**
- **系统 / 架构（DEPLOYMENT 所述测试范围）：** Windows（建议 WSL2，或原生 Docker）、macOS arm64/x86_64、Linux x86_64/arm64；compose 固定 `platform: linux/amd64`
- **浏览器**（noVNC）：打开 `http://localhost:6080/vnc.html`

### 2. 确切步骤 — Docker Compose（README 推荐）

只需 **Docker/** 目录内容（完整克隆亦可）。构建时在镜像内克隆 VirtualAGC。

```bash
# 获取 Docker 脚本（示例：完整浅克隆）
git clone --depth 1 https://github.com/virtualagc/virtualagc
cd virtualagc/Docker

# 推荐
docker-compose up -d
```

若使用本仓库 submodule：

```bash
cd tools/virtualagc/Docker
docker-compose up -d
```

或纯 Docker（同 Docker/README + 根 README）：

```bash
cd virtualagc/Docker   # 必须进入含 Dockerfile 的目录
docker build -t virtualagc .
docker run -d -p 6080:6080 -p 5900:5900 --name apollo11-demo virtualagc
```

**访问：**

1. 浏览器：**http://localhost:6080/vnc.html**
2. 或 VNC 客户端 → `localhost:5900`

`start.sh` 随后在容器内启动 **`./VirtualAGC`**（fluxbox + Xvfb 1600×900）。

**在 VirtualAGC GUI 中加载阿波罗 11 软件**（据 ibiblio 下载页与主页 “Running the Emulator” / Quick Start — Docker、VM、原生 GUI 相同）：

1. 在 VirtualAGC 窗口使用 **Simulation Type**。
2. 选择阿波罗 11 LM 软件（**Luminary 99** / LUMINARY 99 — 下载页默认示例为 Apollo 11 Lunar Module / LUMINARY 99）**或** 阿波罗 11 Command Module（**Comanche 55** / COMANCHE 55 — 项目资料中 GUI 条目为 “Apollo 11 Command Module”）。
3. 保持启用 **DSKY** 界面（默认配置含 DSKY；下载页示例亦提到遥测）。
4. 点击底部 **Run!**。
5. 主 GUI 窗口消失，出现 **DSKY**（及其他所选外设）。关闭某一仿真窗口（优先关 DSKY）以停止；稍等数秒完成清理。

**已记载的 DSKY 检查**（http://www.ibiblio.org/apollo/index.html — 对 CM Colossus 族与 LM Luminary 族同样适用）：

| 动作 | 按键（AGC 速记） | 预期 |
|------|------------------|------|
| 灯测 | **V35E** | 指示灯亮；88 / +88888 风格数码；VERB/NOUN 闪约 5 秒后停止闪烁 |
| 监视上电以来时间 | **V16N36E** 或 **V16N65E** | R1 小时、R2 分钟、R3 百分之一秒；约每秒更新 |
| 全新启动 / 清显示 | **V36E** | 清除 DSKY「弹球」显示上的垃圾 |

校验套件（可选，同主页）：Simulation Type → **Validation Suite** → Run → OPR ERR 亮、PROG 00 → 按 **PRO** → 数十秒后 PROG **77** + OPR ERR = 通过。

**停止容器：**

```bash
docker-compose down
# 或
docker stop apollo11-demo && docker rm apollo11-demo
```

**可选改分辨率**（Docker/README）：编辑 `start.sh` 中一行 `Xvfb :1 -screen 0 1600x900x24 &`，重建（`docker-compose build` 或 `docker build -t virtualagc .`），再启动。download.html 说明：停 GUI、停容器、编辑、重建、重启。

### 3. 预期现象

- noVNC 桌面中的 **VirtualAGC** GUI（仿真类型、接口、**Run!**）。
- Run 之后：仿真 **DSKY**（可选遥测等窗口）。download.html 描述 LUMINARY 99 + DSKY + 遥测为典型布置。
- COMP ACTY / PROG / VERB / NOUN / 寄存器数码响应上述动词。
- 关闭一个仿真窗口后，其余窗口应在短暂延迟后拆除（主页）；避免只关 “Simulation Status”（若出现该管理器问题，download.html 有说明）。

### 4. 常见坑

- **首次构建很慢**（镜像内克隆 + `make`）；之后启动更快。
- 端口 **6080/5900** 已被占用 — 用 `lsof -i :6080` / `:5900` 检查（DEPLOYMENT 排错）。
- 打开错误 URL — 要用 **`/vnc.html`**，不能只开端口根路径。
- Mac/Windows Docker Desktop 内存不足 → 调到 **4GB+**。
- 期待 Orbiter/NASSP 式飞行画面 — 单独的 Virtual AGC 是 AGC/DSKY/外设，不是完整 LM/CM 面板仿真（项目 README / 主页）。
- Docker 亭**无持久化**；配置弄乱了重建容器即可（download.html Docker 节）。
- 默认 VNC 分辨率 **1600×900** 在某些显示器上可能别扭 — 按文档改 `start.sh`。

### 5. 链接

- 仓库：https://github.com/virtualagc/virtualagc
- Docker README：https://github.com/virtualagc/virtualagc/blob/master/Docker/README.md
- Docker DEPLOYMENT：https://github.com/virtualagc/virtualagc/blob/master/Docker/DEPLOYMENT.md
- 下载 / 构建 / VM / Docker 总览：http://www.ibiblio.org/apollo/download.html
- Quick Start（动词、校验）：http://www.ibiblio.org/apollo/index.html

---

## B′) 原生 `make` 构建（摘要 — 官方 Linux 路径）

优先使用上文 Docker。若在宿主机编译，请遵循 **http://www.ibiblio.org/apollo/download.html**（权威；根 README 警告它可能相对网站过时）。

**Linux（该页核实说明：Ubuntu/Mint）：**

一次性软件包（页上示例）：`libsdl1.2-dev`、`libncurses5-dev`、`liballegro4-dev`、`g++`、`libgtk2.0-dev`、`tcl`、`tk`，以及 **wxWidgets 3.2**（优先 3.2 而非 2.8）、Python 3。

```bash
git clone --depth 1 https://github.com/virtualagc/virtualagc
cd virtualagc
make install
# 或
make clean install
```

本仓库 submodule 路径：`cd tools/virtualagc` 后同样执行 `make install`。

**不要**对 `make install` 使用 `sudo`。然后使用生成的桌面图标，或（非官方支持的 Linux 变体）：

```bash
cd ~/VirtualAGC/Resources
../bin/VirtualAGC
```

选择阿波罗 11 LM（Luminary 99）或阿波罗 11 CM（Comanche 55），再 **Run!**，同 B 节。

其他平台（Windows/MSYS2、Mac、FreeBSD 等）在同一下载页有冗长的按 OS 说明 — 请用那些，不要自行发明编译开关。

---

## 备选：VirtualBox 虚拟机（Docker 不方便时）

据 download.html：下载 **VirtualAGC-VM64** 虚拟机（压缩约 3.7 GB），安装 VirtualBox + Extension Pack，Machine → Add 该 `.vbox`，修好文中提到的两处设置问题，登录 **virtualagc** / **virtualagc**，从桌面运行 **VirtualAGC**。比 Docker 更重，但最接近开箱即用的完整项目桌面。

---

## 快速对比

| 路径 | 安装成本 | 适合 |
|------|----------|------|
| **A webAGC 托管演示** | 无 | 几分钟内试 Luminary099 / Comanche055 |
| **B Docker VirtualAGC** | Docker + 首次镜像构建 | 本地 GUI DSKY + 任务选择，少装宿主机依赖 |
| **B′ 原生 make** | 开发包 + 编译 | 开发者 / 无 Docker |
| **VM** | 大下载 + VirtualBox | 不编译也能用完整项目桌面 |
