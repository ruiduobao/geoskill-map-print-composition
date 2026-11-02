---
name: geoskill-map-print-composition
description: 'Compose multi-layer maps with cartographic decoration and high-resolution render to TIFF or PDF'
---

# 地图打印合成 | Map Print Composition

Print-oriented high-resolution map composition: the colored terrain layer and Horn hillshade are combined with **multiplicative blending** (shaded relief); arbitrary RGB layers can then be overlaid on top (alpha compositing), producing a georeferenced 3-band RGB GeoTIFF and a PDF.

Suitable for producing basemaps for publication-grade topographic maps, wall maps and atlases.

## Core Algorithm / 核心算法

dem_to_color(normalization+colormap) → horn_hillshade → hillshade_blend multiplicative blending (ambient+shade) → optional alpha_composite overlay → uint8 RGB GeoTIFF.

## Dependencies / 依赖

```bash
pip install numpy rasterio scipy matplotlib geopandas shapely pillow
```

## Usage / 使用方法

### Example 1 (synthetic data, offline)

```bash
python geoskill-map-print-composition.py --bbox 116.0 39.0 117.0 40.0 --synthetic --output-dir ./out
```

### Example 2 (high-dpi printing)

```bash
python geoskill-map-print-composition.py --input dem.tif --dpi 300
```

### Example 3 (overlay layer alpha)

```bash
python geoskill-map-print-composition.py --input dem.tif --overlay landcover.tif --overlay-alpha 0.5
```

### Example 4 (custom illumination)

```bash
python geoskill-map-print-composition.py --input dem.tif --azimuth 270 --altitude 40 --ambient 0.1
```

### Example 5 (synthetic shaded relief)

```bash
python geoskill-map-print-composition.py --bbox 116 39 117 40 --synthetic --zfactor 2
```

## Output / 输出

| File | Format | Description |
|---|---|---|
| `print_map.tif` | GeoTIFF | 3-band RGB print raster (main/verifiable deliverable) |
| `print_map.pdf` | PDF | Layout PDF |
| `print_meta.json` | JSON | Illumination/overlay/statistics |

Each run also produces `output-manifest.json` (run manifest).

## Data Source / 数据源 / Source

Local GeoTIFF / vector files; `--synthetic` mode generates physically consistent simulated data, fully offline.

## Privacy / 隐私声明 / Privacy

- Runs offline by default; `--synthetic` mode requires no network at all.
- All processing is performed locally; no user data is uploaded.

## License / License

MIT

---

> 中文完整版：需要时再读 [references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)，不要默认全量加载。
