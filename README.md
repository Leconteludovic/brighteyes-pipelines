# brighteyes-pipelines

BrightEyes ISM/FLIM analysis pipelines for the **5×5 SPAD array** (Genoa Instruments PRISM) on a Leica SP5 two-photon stand.

Developed by **Ludovic Leconte** — Institut Pasteur de Montevideo  
In collaboration with the [Vicidomini Lab](https://www.iit.it/it/research/groups/computational-optical-nanoscopy) (IIT Genoa) — [BrightEyes project](https://github.com/VicidominiLab/BrightEyes-MCS)

---

## Contents

### `APR_Reconstruction_BATCH_v6_EN.ipynb`

Jupyter notebook for **batch ISM/APR post-processing** of `.h5` files acquired with BrightEyes-MCS.

For each `.h5` file in a selected folder, the notebook produces:

| Output | Description |
|---|---|
| `*_images.png` | Confocal open pinhole / close pinhole / ISM+APR comparison panel |
| `*_shifts_full.png` | Shift vectors scatter + fingerprint (%) + 3 quivers (full / even / odd timebins) |
| `*_shifts_stability.png` | Stability diagnostic: (full − even) and (full − odd) deviations per channel |
| `*_frc.png` | FRC curves (timebin split, Vicidomini method) for confocal and ISM+APR |
| `*_summary.png` | Bar charts: FRC resolution and APR gain per file |
| `*_confocal_open.tif` | Summed confocal image (open pinhole) |
| `*_confocal_close.tif` | Central channel image (close pinhole) |
| `*_ism_apr.tif` | ISM+APR reconstructed image |
| `*_channels_raw_25ch.tif` | All 25 SPAD channels (raw) |
| `*_channels_apr_25ch.tif` | All 25 SPAD channels (APR-reassigned) |
| `*_diagnostic.csv` | Per-file metrics: pixel size, dwell time, FRC resolution, APR gain |
| `BATCH_summary.csv` | Summary table across all files |
| `BATCH_summary.png` | Summary bar charts across all files |

**Key parameters (cell 2):**
- `USF = 10` — upsampling factor for cross-correlation (APR)
- `REF_CHANNEL = 12` — central pixel of the 5×5 SPAD array
- `SHOW_FIGURES = True` — display figures inline during processing
- `SAVE_TIFF_*` — toggle TIFF exports independently

---

## Installation

Use the [napari-installer](https://github.com/Leconteludovic/napari-installer) companion tool to set up the `brighteyes-env` conda environment (option `[4]`), then launch Jupyter Lab (option `[5]`).

**Manual install:**
```bash
conda create -n brighteyes-env python=3.10 pip
conda activate brighteyes-env
pip install brighteyes-ism tifffile matplotlib jupyterlab h5py
```

---

## Usage

1. Open Jupyter Lab in the `brighteyes-env` environment
2. Open `APR_Reconstruction_BATCH_v6_EN.ipynb`
3. Run all cells — a dialog window opens to select the folder containing `.h5` files
4. Files named `*_calib*`, `*_irf*`, `*_ref*` are automatically excluded
5. Results are saved in a `diagnostic/` subfolder

---

## Hardware context

- **Detector**: Genoa Instruments PRISM (5×5 SPAD array)
- **Microscope**: Leica SP5 stand, galvo-galvo ScannerMAX
- **Laser**: Coherent InSight X3 (two-photon)
- **Software**: BrightEyes-MCS (IIT Genoa)
- **Platform**: MicroPICell — Institut Pasteur de Montevideo / Nantes Université (France BioImaging)

---

## References

- Castello et al., *Nature Methods* (2019) — ISM with SPAD array
- Vicidomini et al., BrightEyes-MCS — https://github.com/VicidominiLab/BrightEyes-MCS
- FRC method: Banterle et al. / Vicidomini lab (timebin odd/even split)
