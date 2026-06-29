# Baidu → Google Maps Coordinate Converter

A zero-dependency, single-file browser tool that converts Baidu Maps coordinates to WGS-84 (Google Maps standard). Handles the full conversion pipeline — Baidu Mercator → BD-09 → GCJ-02 → WGS-84 — with iterative inverse correction for sub-50m accuracy.

---

## Why this exists

Baidu Maps uses two proprietary coordinate systems — **BD-09** (lat/lng) and **Baidu Mercator (MC)** — which are deliberately offset from the global WGS-84 standard. Coordinates copied from Baidu URLs or exports cannot be dropped directly into Google Maps; they land hundreds of meters from the actual location. This tool corrects that.

---

## Features

- **4 input modes** — paste Baidu URLs, enter BD-09 lat/lng, input raw Mercator XY, or batch-process via CSV
- **Full pipeline conversion** — Baidu MC → BD-09 → GCJ-02 → WGS-84
- **Iterative inverse algorithm** — 6-iteration correction for sub-50m accuracy globally
- **Region-aware** — auto-detects Hong Kong, Macau, Taiwan, and locations outside mainland China and skips the GCJ-02 scramble step where it doesn't apply
- **Direct Google Maps links** — every result includes a clickable "Open ↗" link
- **CSV export** — download all results with BD-09, GCJ-02, WGS-84, region, and Google Maps URL columns
- **No backend, no API, no dependencies** — runs entirely in the browser from a single `.html` file

---

## Conversion Pipeline

```
Baidu URL / MC XY  →  BD-09 lat/lng  →  GCJ-02  →  WGS-84
```

| Step | Description |
|---|---|
| **Baidu MC → BD-09** | Inverse Mercator projection using Baidu's piecewise lookup table |
| **BD-09 → GCJ-02** | Removes Baidu's additional offset layer |
| **GCJ-02 → WGS-84** | Iterative inverse of China's national GCJ-02 scramble (6 iterations) |
| **Region check** | HK / Macau / Taiwan / outside China skip the GCJ-02 step |

---

## Input Modes

### Paste URLs
Paste one or more Baidu Maps URLs directly. The tool extracts the embedded Mercator coordinates from the `@x,y,z` fragment and converts them.

> **Note:** URL coordinates represent the map view center, not the pin — expect 50–200m offset. For exact pin locations, use the BD-09 tab.

### BD-09 Lat/Lng
Paste raw BD-09 coordinates (one `lat, lng` pair per line). Optionally provide a matching list of asset names.

### Mercator XY
Enter a single Baidu Mercator X/Y pair manually, with an optional label.

### Batch CSV
Paste a CSV where each row is either a Baidu URL or a `name, lat, lng` triplet. Mixed input is supported.

---

## Output

Each converted result shows:

- Original BD-09 coordinates
- Converted WGS-84 coordinates
- Region flag (if outside mainland China)
- Clickable Google Maps link
- Copy-to-clipboard button

Results can be exported as a CSV with all intermediate coordinate stages included.

---

## Usage

1. Download `baidu-to-google-converter.html`
2. Open it in any modern browser (no server needed)
3. Paste your Baidu URLs or coordinates and click **Convert**

---

## Accuracy

The GCJ-02 → WGS-84 step uses 6 iterations of Newton-style inverse correction, typically converging to within a few centimetres. Real-world accuracy is bounded by the Baidu URL coordinate precision (~50–200m for view-center URLs, full precision for direct BD-09 input).

---

## Browser Support

Works in all modern browsers. No external dependencies, no network requests, no data leaves your machine.

---

## License

MIT
