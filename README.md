# 焦距 × 像素 × 距离 选型参考工具

> CCTV 摄像机选型参考工具 — 焦距、像素、DORI 距离、盲区 一站式查询
>
> Camera Selection Reference — Focal / Pixel / DORI Distance / Blind Zone

[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)
[![Standard: IEC 62676-4](https://img.shields.io/badge/Standard-IEC%2062676--4-orange.svg)]()
[![No Build](https://img.shields.io/badge/build-none-success.svg)]()
[![Single File](https://img.shields.io/badge/file-single%20HTML-brightgreen.svg)]()

## 项目简介

弱电安防（ELV）项目选型时，经常需要根据场景反推摄像机的焦距和像素配置。这套工具基于 **IEC 62676-4 DORI 标准**（业界主流的"探测/观察/识别/辨识"距离定义）计算并可视化焦距、像素、距离三者关系。

包含两部分：

- **[焦距像素距离对照表.md](焦距像素距离对照表.md)** — Markdown 数据表，附速查指南
- **[焦距像素距离-查询工具.html](焦距像素距离-查询工具.html)** — 单文件 HTML 工具（无需安装，双击打开）

## 功能特性

### 📐 视场角分析（Tab 01）

侧视图可视化显示摄像机在 2.8m 安装高度下的视场覆盖：

- **DORI 分层渲染** — 地面 4 段彩色带（红 I / 橙 R / 黄 O / 绿 D）展示实际可用范围
- **FOV 边线** — 镜头视野的上下边界（淡蓝虚线）
- **盲区标注** — 红色斜纹三角 + 自动计算的盲区距离
- **可调参数**：
  - 焦距（2.8 / 4 / 6 / 8 / 12 mm）
  - 像素（2MP / 4MP / 8MP）
  - 安装高度（0.5 ~ 10 m）
  - 俯角（0° ~ 80°，AUTO 模式按焦距推荐）
  - 显示距离（5 ~ 150 m）

### 🎯 部署模板（Tab 02）

7 个 Tendo 实际项目场景预设：

- 电梯厅 / 走道 / 大堂 / 收银台
- 停车场出入口 / 园区周界 / 道路卡口

点击场景卡片自动跳到数据矩阵并预填筛选。

### 📊 数据矩阵（Tab 03）

15 条完整数据（5 焦距 × 3 像素）：

- 焦距 / 像素多选筛选
- 水平视场角 / 俯角 / 盲区
- DORI 4 级距离（探测/观察/识别/辨识）
- 适配场景说明
- 超 50m 自动标 ⚠️

### ⚖️ 并排对比（Tab 04）

A / B 双配置对比，差值用颜色标注（绿色更优 / 红色更差）。

## 快速使用

```bash
# 方式 1：直接打开 HTML（无需任何依赖）
双击 焦距像素距离-查询工具.html

# 方式 2：克隆仓库
git clone https://github.com/cailleachzou/cctv-focal-distance-tool.git
cd cctv-focal-distance-tool
# 浏览器打开 HTML 文件
```

**零依赖** — 单文件 HTML，Google Fonts 通过 CDN 加载（断网时降级为系统字体）。

## 技术规格

| 参数 | 取值 | 说明 |
|---|---|---|
| 传感器 | 1/2.8"（Sensor_W = 5.12mm） | Hikvision / Dahua 主流 |
| 焦距 | 2.8 / 4 / 6 / 8 / 12 mm | 常见定焦镜头 |
| 像素 | 2MP (1920H) / 4MP (2560H) / 8MP (3840H) | 1080P / 2K / 4K |
| 标准 | IEC 62676-4 | DORI 国际标准 |

### DORI 像素密度标准

| 等级 | 英文 | 含义 | 像素密度 |
|---|---|---|---|
| **D** 探测 | Detection | 能"看到有东西" | 25 px/m |
| **O** 观察 | Observation | 能看清轮廓/姿态 | 62 px/m |
| **R** 识别 | Recognition | 能认出熟人 | 125 px/m |
| **I** 辨识 | Identification | 能辨认陌生人五官 | 250 px/m |

### 核心公式

```
水平视场角  H-FOV = 2 × arctan(5.12 / (2 × f))
垂直视场角  V-FOV = 2 × arctan(3.84 / (2 × f))
DORI 距离  D = H_Pixels / (2 × tan(H-FOV/2) × DORI_px/m)
盲区       B = H / tan(α + V-FOV/2)
```

`H` = 安装高度，`α` = 俯角，`f` = 焦距

## 文件结构

```
cctv-focal-distance-tool/
├── README.md                              ← 本文件
├── LICENSE                                ← MIT 许可证
├── .gitignore                             ← Git 忽略配置
├── 焦距像素距离对照表.md                  ← Markdown 数据表 + 速查指南
└── 焦距像素距离-查询工具.html             ← 单文件 HTML 查询工具
```

## 浏览器兼容性

- Chrome / Edge / Firefox / Safari 现代版本（2020+）
- 移动端响应式布局（768px 以下自动堆叠）
- IE 不支持（使用了 CSS 变量、Grid、ES6+）

## 数据来源

- **DORI 标准**：IEC 62676-4 (https://www.iec.ch/)
- **镜头参数**：Hikvision / Dahua / Uniview 官方规格书
- **典型俯角假设**：基于中近距离常见安装场景（非强制）

## 实际项目注意事项

- 本表为**理论计算值**（理想光学 + 标准 DORI），实际项目应留 30-50% 裕量（雾天、逆光、镜头畸变会降低有效距离）
- 镜头标注的焦距可能为"等效焦距"（厂商虚标），需以实测视场角为准
- 变焦镜头可覆盖多档，但成本是定焦 3-5 倍，选型时优先定焦
- 1/3" 传感器的视场角比 1/2.8" 小约 6%，DORI 距离相应降低 6%

## 路线图

- [x] 基础数据表（15 组合）
- [x] 视场角示意图（侧视图 + DORI 分层）
- [x] 部署模板（7 预设）
- [x] 并排对比（A/B 差值）
- [x] 可调安装高度 / 俯角
- [ ] 1/3" 传感器切换
- [ ] 镜头畸变模拟
- [ ] PDF 导出（用于方案附件）
- [ ] 多语言（英文界面）

## 贡献

欢迎提交 Issue / Pull Request：
- 新场景模板（停车场 / 电梯 / 走廊 等）
- 不同传感器尺寸的对比
- 主流厂商镜头的实测 DORI 数据

## 许可证

[MIT](LICENSE) © DUDU & Cailleach

---

**致谢**：本工具在 Tendo Technology 上海团队多个实际项目中迭代验证。数据计算基于公开行业标准，可放心用于方案设计。
