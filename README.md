# PTU FLIM Channel/Window Plotter

This repository contains a small utility script to quickly visualize which FLIM channels were active in a PicoQuant PTU file and to explore time-delay (dtime) windows. It produces:

- A log-scale histogram of the PTU counts summed over channels.
- A grid of images: rows = selected dtime windows, columns = detector channels.

Script: `plot_ptu_channel_windows.py`

## Features

- Load a PTU file via a `PtuFile` interface.
- Compute simple, evenly spaced dtime windows (configurable count).
- Sum frames and dtime-bins into a 2D image for each channel and window.
- Save publication-ready PNGs.

## Requirements

- Python 3.9+ (tested versions may vary)
- numpy
- matplotlib
- ptufile (provides `PtuFile` for PTU file handling)

## Installation

This script is based on [PicoQuant and  related PTU files](https://github.com/cgohlke/ptufile/tree/main), therefore it is necessary to install the following dependencies:

```bash
python -m pip install -U "ptufile[all]"
```

Install all dependencies using pip:

```bash
pip install -r requirements.txt
```

Or install them individually:

```bash
pip install numpy matplotlib ptufile
```

## Usage

1. Place or reference your PTU file (e.g., `FLIM_20250715-170852/RawImage.ptu`).
2. Open `plot_ptu_channel_windows.py` and adjust:
   - `filename`: path to the PTU file.
   - `N_WINDOWS`: number of evenly spaced dtime windows.
   - `channel_ids`: list of channel indices to visualize.
3. Run the script:

```bash
python plot_ptu_channel_windows.py
```

## Output

- `ptu_histogram_log.png`: log-scale histogram of counts summed over channels.
- `channels_overview_grid.png`: grid of images with rows = windows and columns = channels.

## Configuration Details

- Windowing: `compute_windows_from_hist()` currently splits the histogram range into `N_WINDOWS` equal-width windows. You can replace this with peak-based window detection if desired.
- Performance: The script decodes only the requested dtime window and integrates frames to keep memory usage manageable. Logging provides timing for decode and reduction steps.

## Troubleshooting

- Import error for `ptufile`: Ensure you've installed all dependencies with `pip install -r requirements.txt`.
- No channels or unexpected shapes: The script logs `ptu.shape`, `frames`, `channels`, and `bins` to help verify file contents.
- Large files: Reduce `N_WINDOWS`, subset `channel_ids`, or run on a machine with more RAM.

## Contributing

Issues and pull requests are welcome. Please include a short description, steps to reproduce (if applicable), and environment details.

## License

Specify your preferred license (e.g., MIT, Apache-2.0). If you want, I can add a `LICENSE` file for you.