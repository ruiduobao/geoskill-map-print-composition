# Map Print Composition (geoskill-map-print-composition)

> Compose multi-layer maps with cartographic decoration and high-resolution render to TIFF or PDF

---

## 1. Overview

Print-oriented high-resolution map composition: a color terrain layer and a Horn hillshade are combined via **multiplicative blending** (shaded relief), with optional overlay of arbitrary RGB layers (alpha compositing), outputting a georeferenced 3-band RGB GeoTIFF and a PDF. Suitable for producing basemaps for publication-grade topographic maps, wall maps, and atlases.

## 3. Quick Start

```bash
pip install -r requirements.txt
python geoskill-map-print-composition.py --bbox 116 39 117 40 --synthetic --output-dir ./out
```

## 4. CLI Parameters

Run `python <skill>.py --help` for the full list. Common parameters:

| Parameter | Type | Description |
|---|---|---|
| `--bbox` | `float[4]` | WGS84 bounding box `min_lon min_lat max_lon max_lat` |
| `--input` | `path` | Local input file (GeoJSON/GeoTIFF/etc.) |
| `--output-dir` | `path` | Output directory (default `./output`) |
| `--synthetic` | `flag` | Use synthetic data instead of real input |
| `--quiet` | `flag` | Suppress non-essential stdout |

## 5. Input / Output

| File | Format | Description |
|---|---|---|
| `print_map.tif` | GeoTIFF | 3-band RGB print raster (primary/verifiable output) |
| `print_map.pdf` | PDF | Layout PDF |
| `print_meta.json` | JSON | Lighting / overlay / statistics |

Each run also produces `output-manifest.json` (run manifest).


## 6. Technical Principle

dem_to_color(normalize + colormap) → horn_hillshade → hillshade_blend multiplicative blend (ambient + shade) → optional alpha_composite overlay → uint8 RGB GeoTIFF.

## 8. License

MIT License. See [`LICENSE`](./LICENSE) for full text.

---

> 中文完整版：[references/SKILL.zh-CN.md](references/SKILL.zh-CN.md)
