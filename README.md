![GridViewer screenshot](https://github.com/user-attachments/assets/aec7ca60-bd83-4831-a32e-7a89412bebae)

# GridViewer

GridViewer is a browser-based tool for displaying worked and confirmed Maidenhead grid squares from ADIF log files on an interactive map.

It uses OpenStreetMap and Leaflet for the map display. The grid mapping approach and parts of the original idea were inspired by Jeffrey B. Otterson, N1KDO, and his open-source project [lotw-gridmapper](https://github.com/n1kdo/lotw-gridmapper).
His `lotwreport.py` file is used as is for for fetching data from the ARRL LoTW lotwreport.adi web service.

[Installation instructions](https://github.com/awandahl/gridviewer/blob/main/Installation.md)

## Functions

- Displays worked grid squares on an interactive world map.
- Uses `wsjtx_log.adi` as the source for worked QSOs.
- Uses `lotwreport.adi` as the source for LoTW-confirmed QSOs.
- Shows worked grids in red and confirmed grids in green.
- Calculates and displays the number of worked grids, confirmed grids, confirmation percentage, and total QSO count for the current filter selection.
- Filters results by band, mode, and year.
- Provides "Select All" and "Reset" controls for band, mode, and year filters.
- Shows station details for each grid square on hover.
- Marks confirmed QSOs in the hover popup when they match the current band, mode, year, grid, and callsign combination.
- Includes a callsign search field that searches within the currently selected filters.
- Shows a result panel for callsign search with band, mode, date, grid, callsign, and LoTW status.
- Moves the map to the first matching grid found by a callsign search and highlights that grid.
- Supports optional display of the Maidenhead grid overlay.
- Supports switching the Maidenhead overlay color between red and black.
- Reloads the ADIF files automatically every 30 minutes.
- Handles three operating cases: both ADIF files present, only `wsjtx_log.adi` present, or only `lotwreport.adi` present.

## Input files

GridViewer looks for the following files in the same location as `gridviewer.html`:

- `wsjtx_log.adi` — worked QSOs.
- `lotwreport.adi` — confirmed QSOs from LoTW.

If both files are present, the map shows both worked and confirmed status.

If only `wsjtx_log.adi` is present, the map shows worked QSOs only.

If only `lotwreport.adi` is present, the file is used both as the confirmation source and as the data source for the map and filters.

If neither file is present, GridViewer opens with an empty map and a message indicating that no ADIF files were found.

## Display and filtering

The interface contains three filter groups:

- Band
- Mode
- Year

The map, counts, tooltips, and callsign search results are updated from the current filter selection.

The default selections in the current version are:

- Band: `6M`
- Mode: `FT8`
- Year: all years found in the log

## Grid square details

Hovering over a highlighted grid square shows:

- Grid identifier
- Whether the grid is confirmed in LoTW for the current selection
- Callsigns found in that grid
- Year or years worked for each callsign
- A check mark for years that correspond to a confirmed matching QSO

## Callsign search

The callsign search field is applied to the currently selected band, mode, and year filters.

The result list shows:

- Band
- Mode
- Date and time
- Grid square
- Callsign
- LoTW confirmation status

When one or more matches are found, the map centers on the first matching grid and highlights it.

## Purpose

GridViewer was written as a lightweight alternative for viewing worked grids from ADIF files in a web browser, including on lower-power systems.

It does not depend on a separate application framework. In normal use it only requires the HTML file, the ADIF file or files, and a web server or other local method for serving the files to a browser.

## Notes

- The map uses OpenStreetMap tiles and Leaflet.
- The Maidenhead overlay uses the Leaflet.Maidenhead plugin by HA8TKS.
- ADIF parsing is done in the browser.
- The current implementation standardizes `FT4` and `FT8` from `SUBMODE` where applicable.

Anders Wändahl, SM0HPL
