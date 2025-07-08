# Axon Segmentation via Color Intensity on Xenium Images
This project demonstrates a complete pipeline for segmenting human axons based on the intensity differences between DAPI and 18S channels from 10x Genomics Xenium OME-TIFF images. It uses interactive visualization and color thresholding to identify axon-rich regions.

##  Folder Structure
```
axon-segmentation/
├── Input/
│   └── morphology_focus_0000.ome.tif
├── Output/
│   ├── mask_polygons_all_Ipywsettings.geojson
│   └── mask_polygons_Ipywsettings_AreaAbove250.geojson
├── Plots/
│   └── Top_region_plot.png, Right_region_plot.png, ...
├── Axon_Segmentation_Xenium.ipynb # Main Jupyter Notebook
└── README.md
```
## 🎯 Objective

- Segment axons by isolating **18S-rich** but **DAPI-free** regions in spatial transcriptomics images.
- Export detected axon regions as vectorized **GeoJSON** files for downstream analysis.

## Pipeline Workflow

### 1. **Image Loading**
- Load multi-channel OME-TIFF image using `tifffile`.
- Print OME-XML metadata (optional).

### 2. **Channel Extraction**
- Extract two channels for segmentation:
  - `DAPI (Channel 0)`
  - `18S (Channel 2)`

### 3. **Cropping**
- Crop a central square region of the image.
- Additionally extract 4 surrounding regions: **Top, Right, Bottom, Left**.

### 4. **Interactive Thresholding**
- Use `ipywidgets` sliders to adjust min/max thresholds for each channel.
- Preview zoomed-in overlays of:
  - Original Merged (18S & DAPI)
  - Binary Masks (Individual Masks of 18S & DAPI)
  - All combined masks
  - Unique Axon Mask (18S-DAPI)

### 5. **Image Plot Saving**
- Save plots of each region (`Top`, `Right`, etc.) in `Plots/` as `.png`.

### 6. **GeoJSON Mask Export**
- Extract **polygon boundaries** of axon masks using `skimage.measure` and `shapely.
- Based on the min/max thresholds selected in the step 4, apply same on over all image and save the boundaries in GeoJson file format.
- Save:
  - `mask_polygons_all_Ipywsettings.geojson` (all detected regions)
  - `mask_polygons_Ipywsettings_AreaAbove250.geojson` (regions filtered by area ≥ 250 px²)

## Clone & Run the Repository

You can clone this repository using:

```bash
git clone https://github.com/Hemanth-Mydugolam/axon-segmentation.git
```

### Dependencies

Install required Python packages with:

```bash
pip install numpy matplotlib opencv-python tifffile ipywidgets shapely scikit-image geojson
```

### Launch the notebook:
```bash
jupyter notebook Axon_Segmentation_Xenium.ipynb
```

## Results Summary
- Interactive segmentation of axon-specific regions using DAPI/18S thresholds.
- Exported GeoJSON files for spatial vector data.
- Visual validation plots for thresholded masks and overlaps.
- Flexible crop and zoom capability to inspect region of interest.

##  Author
Developed by <a href="https://github.com/Hemanth-Mydugolam" target="_blank">Hemanth Mydugolam</a> for visualizing and segmenting axonal structures using 10x Genomics Xenium spatial transcriptomics data.

## License
MIT License. See LICENSE for full details.
