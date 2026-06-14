![GridViewer Screenshot](https://github.com/awandahl/gridviewer/blob/main/screen_shot.png)

# GridViewer

GridViewer is a browser-based tool for displaying worked and confirmed Maidenhead grid squares from ADIF log files on an interactive map. My live instance running at a Rock 4 SE is available from time to time at http://sm0hpl.tplinkdns.com:8000/

It uses OpenStreetMap and Leaflet for the map display. The grid mapping approach and parts of the original idea were inspired by Jeffrey B. Otterson, N1KDO, and his open-source project [lotw-gridmapper](https://github.com/n1kdo/lotw-gridmapper). His `lotwreport.py` file is used as is for for fetching data from the ARRL LoTW lotwreport.adi web service.

[Installation instructions](https://github.com/awandahl/gridviewer/blob/main/Installation.md)

## Functions

- Displays worked grid squares on an interactive world map.
- Uses `wsjtx_log.adi` as the source for worked QSOs.
- Uses `lotwreport.adi` as the source for LoTW-confirmed QSOs.
- Shows worked grids in red and confirmed grids in green.
- Calculates and displays the number of worked grids, confirmed grids, confirmation percentage, and total QSO count for the current filter selection.
- Filters results by band, mode, and year.
- Provides `Select All` and `Reset` controls for band, mode, and year filters.
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

- `wsjtx_log.adi` — worked QSOs
- `lotwreport.adi` — confirmed QSOs from LoTW

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

## Example LoTW update script

One way to create `lotwreport.adi` is to run a wrapper shell script that calls `lotwreport.py` and writes the output directly to the file used by GridViewer.

Example:

```bash
#!/bin/bash
python3 lotwreport.py \
  --login sm0hpl \
  --password '*******' \
  --qso_qsl yes \
  --qso_owncall sm0hpl \
  --qso_startdate 2015-01-01 \
  --qso_enddate 2999-12-31 \
  --qso_band 6M \
  --qso_qsldetail yes > lotwreport.adi
```

This example is limited to `6M`, because that is the band currently of interest in this setup. The same method can be used with different bands or date ranges.

The script writes the returned LoTW ADIF data to `lotwreport.adi`, replacing the previous file.

## Example cron job

The shell script above can be started from `cron` every 30 minutes.

Example crontab entry:

```cron
*/30 * * * * flock -n /tmp/lotwreport.lock /home/aw/hamradio/install/gridviewer/run_lotwreport.sh >> /home/aw/hamradio/install/gridviewer/lotwreport_cron.log 2>&1
```

This does the following:

- `*/30 * * * *` runs the job every 30 minutes
- `flock -n /tmp/lotwreport.lock` prevents overlapping runs by using a lock file and exiting immediately if a previous run is still active
- `/home/aw/hamradio/install/gridviewer/run_lotwreport.sh` runs the update script
- `>> /home/aw/hamradio/install/gridviewer/lotwreport_cron.log 2>&1` appends both normal output and error output to a log file for later inspection

This is only one example of how `lotwreport.adi` can be maintained. GridViewer itself only requires that the file exists and is refreshed by some external method.

## Purpose

GridViewer was written as a lightweight alternative for viewing worked grids from ADIF files in a web browser, including on lower-power systems.

It does not depend on a separate application framework. In normal use it only requires the HTML file, the ADIF file or files, and a web server or other local method for serving the files to a browser.

## Notes

- The map uses OpenStreetMap tiles and Leaflet.
- The Maidenhead overlay uses the Leaflet.Maidenhead plugin by HA8TKS.
- ADIF parsing is done in the browser.
- The current implementation standardizes `FT4` and `FT8` from `SUBMODE` where applicable.

Anders Wändahl, SM0HPL
