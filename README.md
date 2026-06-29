# Baidu-Coordinate-Converter
A single-file browser tool that converts Baidu Maps coordinates (Mercator MC, BD-09 lat/lng) to WGS-84 for Google Maps. Supports URL paste, manual entry, and batch CSV input. Handles the full BD-09 → GCJ-02 → WGS-84 pipeline with iterative inverse for sub-50m accuracy, including region detection for Hong Kong, Macau, and Taiwan.
