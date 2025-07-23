## Key Concepts

- **Grid Square**: A geographic area defined by a 4-character code, used in the amateur radio community.
- **QSO**: A radio contact (log entry).
- **Confirmed**: Contact is verified (e.g., by the LoTW system).


## File Structure and Flow

### 1. HTML Structure

- Sets up:
    - **Header, logo, and map container**.
    - **Filter checkboxes** (for bands, modes, years).
    - **Footer** (with GitHub link and callsign search).
    - **Results popup** (shows details when you search for a station).


### 2. Styling (CSS)

- Ensures map and interface look clean and modern.
- Uses specific colors for "worked" (`#ff0000`/red) and "confirmed" (`#00b300`/green) grid squares, aligning with common amateur radio color conventions[^4].


### 3. JavaScript (Main Logic)

#### Core Data

- `allQsos`: All the user's QSO records.
- `confirmedGridBandModeYearSet`: Set of grid/band/mode/year combinations that are confirmed.
- `confirmedQsoSet`: Set of individual confirmed QSOs (for detailed verification).
- `gridToCallsigns`: Links grid squares to the callsigns worked there.
- `confirmedFilteredGrids`: The set of confirmed grids **after current filters** are applied.
- `gridRects`: Map of grid square codes to their drawn rectangle objects on the map.
- `highlightedGridSquare`: The currently highlighted rectangle (e.g., after a callsign search).


### Main Functions \& Their Relations

**(Grouped by Purpose)**

#### A. Data Loading and Parsing

- **`parse_adif_line(block)`**: Parses a block of ADIF text (amateur radio contact format) into a JavaScript object with field/value.
- **`processAdiLines(text)`**: Processes the main ADIF file (all QSOs), fills `allQsos` array, tracks which bands, modes, and years exist, sets up the initial filters, and links grid squares to callsigns and years.
- **`processConfirmedAdi(text)`**: Parses the *confirmed* (LoTW) file, filling `confirmedGridBandModeYearSet` and `confirmedQsoSet` for confirmed status checks.


#### B. Filters UI

- **`generateBandCheckboxes(bandsFound)` / `generateModeCheckboxes(modesFound)` / `generateYearCheckboxes(yearsFound)`**: Dynamically creates checkbox controls for each type of filter, based on the ADIF files' contents. Each controls a group of checkboxes for filtering bands, modes, or years, and wires up their event handlers.
- **`getSelectedBands()`, `getSelectedModes()`, `getSelectedYears()`**: Helpers that return an array with all currently checked filter values.


#### C. Grid/Map Display

- **`gridToCoordinates(gridSquare)`**: Converts a 4-character grid locator (e.g., `JO65`) to map coordinates so the correct area is shown.
- **`drawMap()`**: Initializes a new Leaflet map, resets the grid overlays, and adds the OpenStreetMap map tiles.
- **`addSquare(map, gridSquare, callsignYears, isConfirmed)`**: Draws a rectangle on the map for the grid, colors it based on confirmation, adds a clickable/hover label, and attaches a tooltip showing callsigns and years.


#### D. Map Updates (and Filtering)

- **`updateMap()`**: Master function. Reads current filter selections, determines which grids and QSOs match, computes confirmation stats, draws the colored/labelled grid rectangles on the map, and updates the legend and summary.
    - **Relation**: Called after any change in filters, or after ADIF data loads.


#### E. Callsign Search

- **`searchQsosByCallsign(callInput)`**: Searches the QSO records for contacts matching the user's search input, respecting filters.
- **`doCallsignSearch()`**: Uses the above to display the results in the popup, draws a table of matches, and highlights the relevant grid(s) on the map.
- **`focusOnGrid(gridSquare)`**: Pans and zooms the map to a specific grid, and highlights it in yellow.


#### F. Page/Map Initialization

- **`boot()`**: Loads radio log files asynchronously (`wsjtx_log.adi` and `lotwreport.adi`), processes their data through the above functions, and initializes map + filters.
    - Called immediately on page load and every 30 minutes (auto-refresh).


### Event Handlers and Interface Logic

- **Checkboxes for band, mode, year** update the map immediately on change.
- **Enter in search box** triggers callsign lookup.
- **Clicking 'close' on popup** hides it and resets any highlighted grid.


## High-Level Relationships

- **Data Loading (`boot`) -> Data Parsing (`processAdiLines`, `processConfirmedAdi`) -> UI Generation (`generateBand/Mode/YearCheckboxes`) -> Map Redrawing (`updateMap`)**
- Every interaction (filter change, search, data refresh) flows through this chain.


## In Plain English: How the App Works

1. **Loads two log files**: one for all worked QSOs, another for confirmed QSOs.
2. **Parses** each contact for band, mode, year, callsign, and grid.
3. **Displays a map**: each grid square is colored if worked, green if confirmed[^2][^4].
4. **Lets the user filter**: see which grids were worked or confirmed by specific band, mode, or year.
5. **Shows callsign details**: search by callsign to see all grids worked, confirmed, and QSO details, and zoom to them.
6. **Auto-refreshes**: keeps map up to date if new log files are received.

## Example: What happens when you select a band or mode?

- The filters call `updateMap()`, which rebuilds the set of eligible grid squares and QSOs based on those selections, recalculates confirmations, and redraws the map and statistics accordingly.
