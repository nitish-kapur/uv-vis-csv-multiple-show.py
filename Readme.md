# UV-Vis Plotter from CSV — Multiple Show

A Python script that batch processes UV-Vis absorbance spectra from CSV files and displays all plots simultaneously in interactive matplotlib windows.

## Author

**Nitish Kapur**<br>
GitHub: [github.com/nitish-kapur](https://github.com/nitish-kapur)

## Expected Input Format

The script expects CSV files exported from a UV-Vis spectrophotometer. Each file must contain an `XYDATA` marker line, after which the spectral data begins in two comma-separated columns:

    ... (metadata — instrument name, date, settings, etc.) ...
    XYDATA
    400.0, 0.523
    401.0, 0.511
    402.0, 0.498
    ...

| Element | Description |
|---|---|
| Metadata lines | Any number of lines before `XYDATA` — automatically ignored by the parser |
| `XYDATA` marker | Signals the end of metadata; data parsing begins on the next line |
| Column 1 | Wavelength (nm) — must be a numeric float |
| Column 2 | Absorbance (A) — must be a numeric float |
| Separator | Comma (`,`) |
| Empty lines | Skipped automatically |
| Malformed lines | Lines with fewer or more than two values are skipped with a console warning |

## Requirements

    pip install pandas matplotlib

## Configuration

The input folder path is hard-coded at the top of the script. Update it to match your directory structure:

    desktop_path = r"C:\Users\Material Science Lab\Desktop"
    input_folder = os.path.join(desktop_path, "raw")

## Usage

1. Place all UV-Vis CSV files in the input folder
2. Run:

    python uv-vis-csv-multiple-show.py

All plots are displayed simultaneously in interactive matplotlib windows once all files have been processed.

## Output

- One interactive matplotlib window per CSV file
- X-axis: Wavelength (nm), inverted as per UV-Vis convention
- Y-axis: Absorbance (A)
- Title: derived from the CSV filename

## Notes

- Unlike the save version of this script, plots are displayed interactively.
- Files that do not contain an `XYDATA` marker or have no valid spectral data are skipped automatically.
- The X-axis is inverted as per UV-Vis spectroscopy convention.
- All plots are held in memory and shown together at the end using a single `plt.show()` call.
