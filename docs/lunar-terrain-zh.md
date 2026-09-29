# 月球地形数据集：用法与下载入口

整理范围：NASA / LOLA / LROC 相关、近期南极与全球常用产品。链接已核对（约 2026-09）。

## 怎么选

| 你的目标 | 用哪份 | 分辨率量级 |
|---------|--------|-----------|
| 全球背景、大尺度制图 | **SLDEM2015** | ~60 m/px 量级（512 ppd 分块更细） |
| Artemis 南极候选着陆区细节 | **SfS SDEM（Bertone 等）** | 5 m/px，照亮区更细 |
| 南极重点着陆点、带误差估计 | **LOLA 5 m 着陆区 DEM** | 5 m/px |
| 南极极区大图（87°–90°S） | **LOLA 5 m 极区 DEM** | 5 m/px |
| 持续更新的测高剖面 / 网格 | **LOLA PDS（EDR/RDR/GDR）** | 随产品而异 |

**坐标系提示（南极高分产品常见）：** 南极极射赤面投影，平面坐标多为米；参考系常见 **MOON_ME**（如 DE421）。落到 GIS 前先读该产品 README / 元数据。

**软件：** QGIS / ArcGIS 直接读 GeoTIFF；PDS `IMG` / GeoJPEG2000 可用 GDAL；立体/SfS 流水线常见 Ames Stereo Pipeline + ISIS。

---

## 1. Artemis 南极 SfS 增强地形（SDEM）— 最近重点

**是什么：** 对 2022 年公布的 **13 个 Artemis III 候选着陆区**，在 LOLA 5 m DEM 上用 **LROC NAC + Shape-from-Shading** 做出更均匀有效分辨率的 **5 m/px SDEM**，并附山体阴影、坡度、粗糙度、与 LDEM 差值等。覆盖约 4500+ km²。照亮区细节更好；永久阴影处仍受影像限制。

**适用：** 着陆区坡度/粗糙度、光照分析、表面作业规划；不要当成全球 DEM。

**下载：**

| 入口 | URL |
|------|-----|
| 产品说明（PGDA） | https://pgda.gsfc.nasa.gov/products/104 |
| 完整数据包（Zenodo） | https://doi.org/10.5281/zenodo.17954508 |

**用法简述：**

1. 打开 Zenodo → 按着陆区下载对应包（含 SDEM 高程栅格、hillshade、orthomosaic、coverage、slope、VRM 等）。
2. 用 QGIS 加载 SDEM GeoTIFF；需要坡度时可直接用归档里的 slope，或在 GIS 里重算。
3. 与纯 LOLA 5 m 对比时，看归档中的 **SDEM−LDEM** 差值图。

**引用：** Bertone et al., *The Planetary Science Journal*, doi:10.3847/PSJ/ae5b70；数据 doi:10.5281/zenodo.17954508。

---

## 2. LOLA 南极着陆区 5 m DEM

**是什么：** 用调整后的 LOLA 激光测高生成的 **5 m/px** 区域 DEM（插值高程），并提供点云、命中计数、坡度、高程/坡度不确定度、以及 clone 集合。格式多为 **GeoTIFF**；点云除外。

**站点示例：** Connecting ridge (Site01)、Shackleton rim (04)、Peak near Shackleton (07)、de Gerlache rim (11)、Leibnitz beta (20)、Malapert massif (23) 等。

**下载：** https://pgda.gsfc.nasa.gov/data/LOLA_5mpp/  
（页面含各 Site 目录与 README。）

**另有更大范围：** **87°–90°S** 的 5 m/px DEM（见 LOLA 数据节点首页说明：https://imbrium.mit.edu/ ）。

**用法简述：**

1. 选 Site → 下 `LDEM`（高程 Z，米）及需要的 `Slope` / 不确定度图。
2. 投影一般为南极极射，X/Y 米，**MOON_ME / DE421**（以站点 README 为准）。
3. 做光照或风险分析时务必看 **不确定度** 与点密度（`LDEC`），稀疏轨道路径上的“平滑”是插值，不是观测。

**文献：** Barker et al. 2021, PSS, doi:10.1016/j.pss.2020.105119。

---

## 3. SLDEM2015（全球融合地形）

**是什么：** **LRO/LOLA + 月亮女神 SELENE Terrain Camera** 共注册后的全球地形；典型垂直精度约 **3–4 m**；提供圆柱投影全球图与高分辨率分块（含 512 ppd tiles）。

**适用：** 全球背景、跨区制图、把其它数据套到 LOLA/GRAIL 大地基准；南极米级着陆设计应改用上面的 5 m / SfS 产品。

**下载：**

| 入口 | URL |
|------|-----|
| PGDA 产品页 | https://pgda.gsfc.nasa.gov/products/54 |
| LOLA 数据节点（目录含 `SLDEM2015`） | https://imbrium.mit.edu/ |
| PDS 说明摘录 | https://pds-geosciences.wustl.edu/lro/lro-l-lola-3-rdr-v1/lrolol_1xxx/document/sldem2015.txt |

节点上还有 **SLDEM2015_SLOPE / SLDEM2015_AZIMUTH** 等派生图。

**用法简述：** 下 GeoJPEG2000 或 IMG → GDAL/QGIS 打开；全球分析用较低 ppd，局部细节用 TILES（512 ppd）。

---

## 4. LOLA PDS 常规归档（持续更新）

**是什么：** 测高原始到高级产品的官方归档：**EDR**（原始）、**RDR**（剖面）、**GDR**（网格）、辐射计、球谐等。PDS 按 LRO 发布周期更新（例如 Release 65 含 2025-10–2026-01 区间数据——以节点公告为准）。

**下载：**

| 入口 | URL |
|------|-----|
| LOLA PDS Data Node（首选，更新快） | https://imbrium.mit.edu/ |
| PDS Geosciences 镜像页 | https://pds-geosciences.wustl.edu/missions/lro/lola.htm |
| 用 ODE 检索下载 | 见上述 Geosciences 页说明 |

**用法简述：** 要最新剖面/任务级产品 → Data Node 或 ODE；要稳定引用的归档副本 → PDS Geosciences 对应 Release。读二进制 RDR 可用节点提供的软件说明。

---

## 5. 相关：米级 LROC NAC DTM（研究补充）

学术论文产出的南极着陆区 **约 1 m 级** SfS/立体 DTM 及不确定度，常见挂在 Zenodo 作为论文补充（例如 Hemmi 等 2025 相关补充数据）。**不是**替代 LOLA 官方大地基准的“唯一官方全球图”；与 NASA PGDA 产品交叉使用时注意配准与引用。

示例补充数据：https://zenodo.org/records/17153447  

---

## 推荐工作流（实操）

1. **定范围：** 全球用 SLDEM2015；南极着陆用 LOLA 5 m → 需要更细地表纹理再叠 SfS SDEM。  
2. **下数据：** 优先 GeoTIFF；记录投影与高程基准。  
3. **GIS：** QGIS 加载 → 派坡度/阴影 → 与 NAC 影像叠合检查。  
4. **写进报告：** 按上表引用论文 + DOI / PGDA 产品页。  
5. **本地大文件：** 体积大，建议按 Site / 分块下载，不要一次拉全节点。

## 本仓库关系

本文件属于 [apollo11-agc-study](https://github.com/huming0618/apollo11-agc-study) 的资料索引；与 AGC 飞行软件无关，供月球地形 / 着陆研究对照使用。

## 更新说明

NASA / PGDA / Zenodo 链接若变更，以官方产品页为准。整理日期：2026-09-29（Asia/Shanghai）。
