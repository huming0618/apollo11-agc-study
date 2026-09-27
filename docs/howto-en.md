# How to run Apollo 11 AGC software (verified from upstream docs)

Sources checked (do not invent beyond these):
- https://github.com/michaelfranzl/webAGC (README + demo/README)
- Live demo: https://michaelfranzl.github.io/webAGC/demo/
- https://github.com/virtualagc/virtualagc (README + Docker/README + Docker/DEPLOYMENT.md + Docker/start.sh)
- http://www.ibiblio.org/apollo/download.html
- http://www.ibiblio.org/apollo/index.html (Quick Start / DSKY verbs)

---

## A) webAGC — browser demo (easiest)

### 1. Prerequisites
- **OS:** any desktop OS (Windows / macOS / Linux).
- **Browser:** a modern browser with WebAssembly support (Firefox, Chrome, Edge, Safari — as noted for Wasm on the Virtual AGC download page). The hosted demo is static HTML/JS/WASM.
- **Optional (local serve only):** recent Node.js. demo/README confirms **v22.22.2**. Browsers require content over **HTTP** (not `file://`) for WebAssembly/modules.

### 2. Exact steps — hosted demo (no install)

1. Open: **https://michaelfranzl.github.io/webAGC/demo/**
2. Under **“Load program into fixed memory”**, choose one of:
   - **Luminary099.bin** — Apollo 11 Lunar Module AGC software
   - **Comanche055.bin** — Apollo 11 Command Module AGC software
   - (Also available: Validation.bin for emulator self-test)
3. Under **CPU manipulation**, click **Run** (or Reset then Run). Virtual AGC’s Wasm notes: load the program **first**, then Run (or Step for single instruction).
4. Use the on-screen **DSKY**:
   - Click keys, **or** type into **“DSKY key input”**:
     - Digits `0`–`9`, `+`, `-`
     - VERB=`v`, NOUN=`n`, CLR=`c`, KEY REL=`k`, ENTR=`e` or Enter, RSET=`r`, PRO=`p`

**Documented sample commands (demo page — both Luminary099 and Comanche055):**
- Lamp test: type **VERB 3 5 ENTR** → keys `v` `3` `5` `e` (or click VERB, 3, 5, ENTR)
- Show uptime (seconds, minutes, hours since start): **VERB 1 6 NOUN 6 5 ENTR** → `v` `1` `6` `n` `6` `5` `e`

**Validation.bin path (demo):** when OPR ERR blinks, press **PRO**; after ~38 seconds, PROG should show **77** (success).

### 2b. Exact steps — run demo locally from repo (optional)

From [demo/README.md](https://github.com/michaelfranzl/webAGC/blob/master/demo/README.md):

```sh
git clone --depth=1 https://github.com/michaelfranzl/webAGC
cd webAGC/demo
npm ci
npm run serve-dev
```

Open the URL printed (e.g. `http://localhost:8000`). Then load Luminary099 / Comanche055 and Run as above.

Build + static serve (same README):

```sh
npm run build
npm run serve-build
```

### 3. What you should see
- **AGC emulator panel:** clock divisor, instructions/sec, Reset / Pause / Step / Run, State.
- **DSKY:** annunciators + PROG / VERB / NOUN / R1–R3 style numeric displays; clickable keypad.
- After **V35E**: lamp test (all indicators / 88 style digits — same idea as Virtual AGC’s V35E on the project home page).
- After **V16N65E**: live time since program start in the registers.
- Live **erasable memory** (octal) and input/output port toggles below.

### 4. Common pitfalls
- Forgetting to **load a .bin into fixed memory** before **Run** (empty/wrong rope).
- Opening `file://.../index.html` locally — modern browsers need an HTTP server for Wasm/modules (demo README + Virtual AGC Wasm section).
- Chromium on Android: demo notes the text key-input field may fail ([Chromium bug 118639](https://bugs.chromium.org/p/chromium/issues/detail?id=118639)); use on-screen DSKY keys.
- Expecting a full spacecraft / flight simulator — webAGC is AGC + DSKY + memory views only.

### 5. Links
- Repo: https://github.com/michaelfranzl/webAGC  
- Demo: https://michaelfranzl.github.io/webAGC/demo/  
- Demo README: https://github.com/michaelfranzl/webAGC/blob/master/demo/README.md  
- Program docs: https://www.ibiblio.org/apollo/

---

## B) VirtualAGC local — Docker preferred

Official docs: Virtual AGC can be deployed with Docker without installing host build deps. The Docker “GUI kiosk” starts **VirtualAGC** in a VNC desktop (noVNC in the browser). Prefer this over native `make` unless you need full native tooling.

### 1. Prerequisites (from Docker/DEPLOYMENT.md)
- **Docker Engine 20.10+** or **Docker Desktop**
- **Docker Compose 2.0+** (bundled with Docker Desktop)
- **≥ 2 GB RAM** available (Desktop: Settings → Resources → Memory; guide suggests **4 GB+**)
- Host ports **6080** (noVNC) and **5900** (VNC) free
- Outbound network to GitHub during **image build** (Dockerfile clones + compiles VirtualAGC)
- **Disk:** DEPLOYMENT suggests **≥ ~5 GB** free for the build
- **OS / arch (tested per DEPLOYMENT):** Windows (WSL2 recommended, or native Docker), macOS arm64/x86_64, Linux x86_64/arm64; compose pins `platform: linux/amd64`
- **Browser** for noVNC: any modern browser to open `http://localhost:6080/vnc.html`

### 2. Exact steps — Docker Compose (recommended in READMEs)

You only need the **Docker/** directory contents (full repo clone also fine). Build clones VirtualAGC inside the image.

```bash
# Obtain Docker scripts (example: full clone)
git clone --depth 1 https://github.com/virtualagc/virtualagc
cd virtualagc/Docker

# Recommended
docker-compose up -d
```

Or plain Docker (same Docker/README + root README):

```bash
cd virtualagc/Docker   # must be in the directory that contains the Dockerfile
docker build -t virtualagc .
docker run -d -p 6080:6080 -p 5900:5900 --name apollo11-demo virtualagc
```

**Access:**
1. Browser: **http://localhost:6080/vnc.html**
2. Or VNC client → `localhost:5900`

`start.sh` then launches **`./VirtualAGC`** in the container (fluxbox + Xvfb 1600×900).

**Load Apollo 11 software in the VirtualAGC GUI** (from ibiblio download page + home “Running the Emulator” / Quick Start — same GUI whether Docker, VM, or native):

1. In the VirtualAGC window, use **Simulation Type**.
2. Select Apollo 11 LM software (**Luminary 99** / LUMINARY 99 — download page default example is Apollo 11 Lunar Module / LUMINARY 99) **or** Apollo 11 Command Module (**Comanche 55** / COMANCHE 55 — GUI entry documented in project sources as “Apollo 11 Command Module”).
3. Keep a **DSKY** interface enabled (default setups include DSKY; download page example also mentions telemetry).
4. Click **Run!** at the bottom.
5. The main GUI window disappears; **DSKY** (and other selected peripherals) appear. Close a simulation window (prefer closing the DSKY) to stop; wait a few seconds for cleanup.

**Documented DSKY checks** (http://www.ibiblio.org/apollo/index.html — works for CM Colossus-family and LM Luminary-family alike):

| Action | Keys (AGC shorthand) | Expected |
|--------|----------------------|----------|
| Lamp test | **V35E** | Annunciators lit; 88 / +88888 style digits; VERB/NOUN flash ~5 s then stop flashing |
| Monitor time since power-up | **V16N36E** or **V16N65E** | R1 hours, R2 minutes, R3 hundredths of a second; updates ~1/s |
| Fresh start / clear display | **V36E** | Clears garbage from DSKY “pinball” display |

Validation suite (optional, same home page): Simulation Type → **Validation Suite** → Run → OPR ERR on, PROG 00 → press **PRO** → after tens of seconds PROG **77** + OPR ERR = pass.

**Stop container:**

```bash
docker-compose down
# or
docker stop apollo11-demo && docker rm apollo11-demo
```

**Optional resolution change** (Docker/README): edit `start.sh` line `Xvfb :1 -screen 0 1600x900x24 &`, rebuild (`docker-compose build` or `docker build -t virtualagc .`), restart. download.html notes: stop GUI, stop container, edit, rebuild, restart.

### 3. What you should see
- noVNC desktop with **VirtualAGC** GUI (simulation type, interfaces, **Run!**).
- After Run: simulated **DSKY** (and optionally telemetry / other windows). download.html describes LUMINARY 99 + DSKY + telemetry as a typical arrangement.
- COMP ACTY / PROG / VERB / NOUN / register digits respond to verbs above.
- Closing one simulation window should tear down the rest after a short delay (home page); avoid only closing “Simulation Status” if that manager bug appears (noted on download.html).

### 4. Common pitfalls
- **First build is slow** (clone + `make` inside image); later starts are faster.
- Ports **6080/5900** already in use — check with `lsof -i :6080` / `:5900` (DEPLOYMENT troubleshooting).
- Opening the wrong URL — use **`/vnc.html`**, not only the port root.
- On Mac/Windows Docker Desktop: insufficient memory → bump to **4GB+**.
- Expecting Orbiter/NASSP-style flight visuals — Virtual AGC alone is AGC/DSKY/peripherals, not a full LM/CM panel sim (project README / home page).
- Docker kiosk has **no persistence**; misconfiguration is reset by recreating the container (download.html Docker section).
- Default VNC size **1600×900** may look odd on some monitors — adjust via `start.sh` as documented.

### 5. Links
- Repo: https://github.com/virtualagc/virtualagc  
- Docker README: https://github.com/virtualagc/virtualagc/blob/master/Docker/README.md  
- Docker DEPLOYMENT: https://github.com/virtualagc/virtualagc/blob/master/Docker/DEPLOYMENT.md  
- Download / build / VM / Docker overview: http://www.ibiblio.org/apollo/download.html  
- Quick Start (verbs, validation): http://www.ibiblio.org/apollo/index.html  

---

## B′) Native `make` build (brief — official Linux path)

Prefer Docker above. If you build on the host, follow **http://www.ibiblio.org/apollo/download.html** (authoritative; root README warns it may be stale vs the website).

**Linux (verified notes on that page: Ubuntu/Mint):**

One-time packages (examples from the page): `libsdl1.2-dev`, `libncurses5-dev`, `liballegro4-dev`, `g++`, `libgtk2.0-dev`, `tcl`, `tk`, plus **wxWidgets 3.2** (prefer 3.2 over 2.8), Python 3.

```bash
git clone --depth 1 https://github.com/virtualagc/virtualagc
cd virtualagc
make install
# or
make clean install
```

Do **not** use `sudo` for `make install`. Then use the created desktop icon, or (unsupported Linux variants):

```bash
cd ~/VirtualAGC/Resources
../bin/VirtualAGC
```

Select Apollo 11 LM (Luminary 99) or Apollo 11 CM (Comanche 55) and **Run!** as in section B.

Other platforms (Windows/MSYS2, Mac, FreeBSD, etc.) have long OS-specific sections on the same download page — use those rather than inventing flags.

---

## Alternative: VirtualBox VM (if Docker is awkward)

From download.html: download **VirtualAGC-VM64** VM (~3.7 GB compressed), install VirtualBox + Extension Pack, Machine → Add the `.vbox`, fix the two noted settings bugs, login **virtualagc** / **virtualagc**, run **VirtualAGC** from the desktop. Heavier than Docker but closest to a full out-of-box desktop.

---

## Quick comparison

| Path | Install effort | Best for |
|------|----------------|----------|
| **A webAGC hosted demo** | None | Try Luminary099 / Comanche055 in minutes |
| **B Docker VirtualAGC** | Docker + first image build | Local GUI DSKY + mission selection without host deps |
| **B′ native make** | Dev packages + compile | Developers / no Docker |
| **VM** | Large download + VirtualBox | Full project desktop without compiling |
