# M57 and M1 Analysis

Reduction and analysis of astronomical observations of **M57** (Ring Nebula, photometry) and **M1** (Crab Nebula, spectroscopy), obtained as part of the TEA (Técnicas Experimentales de Astrofísica) course.

## Contents

| File | Description |
|---|---|
| `M57_photometry_analysis.ipynb` | CCD photometric reduction and flux calibration of M57 (filter B) |
| `M1_spectroscopy_analysis.ipynb` | Spectroscopic reduction, wavelength calibration, and radial-velocity analysis of M1 |

### M57 — Photometry

Full workflow of ground-based CCD photometry, from raw FITS frames to a flux-calibrated science image:

- Reading and inspecting FITS files (image data + header)
- Building master calibration frames: **bias**, **dark**, and **flat**
- Reducing the raw science frames (bias/dark subtraction, flat-fielding)
- Aligning and stacking multiple science exposures (star detection with `DAOStarFinder`, robust affine registration with `RANSAC`)
- Measuring stellar flux and PSF (aperture photometry, radial profile, curve of growth)
- Flux calibration via relative photometry against Gaia-catalog reference stars, converted to the Johnson-Cousins system
- Converting the calibrated image to surface brightness (magnitudes per square arcsecond)
- Measuring the integrated magnitude of the nebula

### M1 — Spectroscopy

Reduction and analysis of long-slit spectroscopic data taken with CAFOS at Calar Alto:

- Bias, dark, and flat-field correction of the raw spectroscopic frames
- Wavelength calibration from arc-lamp emission lines (peak identification + linear pixel-to-wavelength fit)
- Reduction of the nebular spectrum and sky subtraction
- Radial-velocity measurement at seven spatial positions along the slit, from observed line shifts
- Mean radial velocity of the nebula

## Data

The raw FITS frames used in these notebooks are not included in this repository due to their size.

- **M57**: hosted on Google Drive — **[Datos TEA 25/26](https://drive.google.com/drive/folders/1vNXHXhQsEwNVB5EtbLD6huV6AIJr7NwS?usp=sharing)**. Contains the calibration frames (bias, dark, flat) and the science frames organized by observation date (e.g. `2025-11-06`), matching the folder structure expected by the `base` path in `M57_photometry_analysis.ipynb`.
- **M1**: not yet uploaded to a shared location. *(TODO: add a Drive/Zenodo link here once the data is uploaded.)*

For both notebooks, update the `base` path near the top of the notebook to point to your local copy of the corresponding dataset before running.

## Requirements

See [`requirements.txt`](requirements.txt). Install with:

```bash
pip install -r requirements.txt
```

`photutils` and `scikit-image` are only needed for `M57_photometry_analysis.ipynb` (source detection, aperture photometry, image alignment); `M1_spectroscopy_analysis.ipynb` only needs `numpy`, `matplotlib`, `astropy`, and `scipy`.

## Usage

1. Update the `base` path at the top of the relevant notebook to point to your local copy of the data.
2. Run the cells in order — later cells depend on variables computed earlier in the notebook (e.g. `master_bias`, `master_dark`, `master_flat`, `science_calib` in the M57 notebook; `master_bias`, `master_flat_new`, `wavelength_array` in the M1 notebook).
3. In the M1 notebook, the radial-velocity cells for each spatial region use manually identified line positions; adjust these if you are reducing a different dataset.

## Notes

- All code comments, docstrings, and plot labels are in English; variable and function names were kept unchanged from the original working versions.
- In `M57_photometry_analysis.ipynb`, selecting calibration star coordinates requires a one-time manual step: clicking on stars in a displayed image and copying the printed coordinates into the corresponding cell.


