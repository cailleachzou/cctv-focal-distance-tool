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

## 在线预览

🔗 **[在线访问（v1.1 老版本）](https://cailleachzou.github.io/cctv-focal-distance-tool/pre-20260629/)**

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

## 数据来源

- **DORI 标准**：IEC 62676-4 (https://www.iec.ch/)
- **镜头参数**：Hikvision / Dahua / Uniview 官方规格书
- **典型俯角假设**：基于中近距离常见安装场景（非强制）

## 实际项目注意事项

- 本表为**理论计算值**（理想光学 + 标准 DORI），实际项目应留 30-50% 裕量（雾天、逆光、镜头畸变会降低有效距离）
- 镜头标注的焦距可能为"等效焦距"（厂商虚标），需以实测视场角为准
- 变焦镜头可覆盖多档，但成本是定焦 3-5 倍，选型时优先定焦
- 1/3" 传感器的视场角比 1/2.8" 小约 6%，DORI 距离相应降低 6%

## 贡献

欢迎提交 Issue / Pull Request：
- 新场景模板（停车场 / 电梯 / 走廊 等）
- 不同传感器尺寸的对比
- 主流厂商镜头的实测 DORI 数据

## 许可证

[MIT](LICENSE) © DUDU & Cailleach

---

**致谢**：本工具在 Tendo Technology 上海团队多个实际项目中迭代验证。数据计算基于公开行业标准，可放心用于方案设计。
