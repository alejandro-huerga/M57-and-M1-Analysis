# M57 and M1 Photometric Analysis

Photometric reduction and analysis of astronomical images of the **M57** (Ring Nebula) and **M1** (Crab Nebula), taken as part of the TEA (Técnicas Experimentales de Astrofísica) course.

The pipeline covers the full workflow of ground-based CCD photometry, from raw FITS frames to a flux-calibrated science image:

- Reading and inspecting FITS files (image data + header)
- Building master calibration frames: **bias**, **dark**, and **flat**
- Reducing the raw science frames (bias/dark subtraction, flat-fielding)
- Aligning and stacking multiple science exposures (star detection with `DAOStarFinder`, robust affine registration with `RANSAC`)
- Measuring stellar flux and PSF (aperture photometry, radial profile, curve of growth)
- Flux calibration via relative photometry against Gaia-catalog reference stars, converted to the Johnson-Cousins system
- Converting the calibrated image to surface brightness (magnitudes per square arcsecond)
- Measuring the integrated magnitude of the nebula (M57)

## Contents

| File | Description |
|---|---|
| `M57_photometry_analysis.ipynb` | Full reduction and photometric analysis of M57 (filter B) |

## Data

The raw FITS frames (bias, dark, flat, and science images) used in this notebook are not included in this repository due to their size (~7 GB). They are hosted on Google Drive:

**[Datos TEA 25/26](https://drive.google.com/drive/folders/1vNXHXhQsEwNVB5EtbLD6huV6AIJr7NwS?usp=sharing)**

This folder contains the calibration frames (bias, dark, flat) and the science frames organized by observation date (e.g. `2025-11-06`), matching the folder structure expected by the `base` path at the top of the notebook. Download the relevant subfolders and update `base` to point to your local copy before running the notebook.

## Requirements

See [`requirements.txt`](requirements.txt). Install with:

```bash
pip install -r requirements.txt
```

## Usage

1. Update the `base` path at the top of the notebook to point to your local copy of the data.
2. Run the cells in order — later cells depend on variables (`master_bias`, `master_dark`, `master_flat`, `science_calib`, etc.) computed earlier in the notebook.

## Notes

- All code comments, docstrings, and plot labels are in English; variable and function names were kept unchanged from the original working version.
- Some cells (e.g. selecting calibration star coordinates) require a one-time manual step: clicking on stars in a displayed image and copying the printed coordinates into the corresponding cell.


