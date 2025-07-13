<img src="https://github.com/user-attachments/assets/276c1bc4-2384-4db7-a174-d0d07c90d47b" alt="gridviewer_screenshots" width="1000">

## What GridViewer Can Do

**GridViewer** is an interactive open source web-based tool designed for ham radio operators to visualize and analyze their worked grid squares from log files. Here’s what you can do with GridViewer:

### Key Features

#### 1. Interactive Grid Map

- Displays all worked grid squares on an interactive map using OpenStreetMap and Leaflet.
- Each grid square is highlighted so you can easily see your coverage.


#### 2. Powerful Filtering

- **Band Filtering:** Instantly filter your contacts by amateur radio band (e.g., 6M, 2M, 20M, etc.) using intuitive checkboxes.
- **Mode Filtering:** Select which transmission modes (e.g., FT8, SSB, CW) to display.
- **Year Filtering:** Focus on contacts made in specific years, or view all years at once.
- **Select All \& Reset:** Quickly select or reset all options in each filter category for fast exploration.


#### 3. Hover-Over Details

- Hover your mouse over any highlighted grid square to see a popup with:
    - The callsigns you have worked in that square.
    - The year(s) each callsign was worked (e.g., "SM0ABC (2024, 2025)").

#### 4. Real-Time Log Updates

- The tool automatically reloads your log file at regular intervals (default: every 30 minutes), so your map stays up to date as you make new QSOs.

#### 5. User-Friendly Interface

- Clean, responsive design that works well on desktops, tablets, and mobile devices.
- All controls are accessible and hopefully intuitive, with clear labels and logical grouping.

## How to Install GridViewer on Linux and Windows

Below are step-by-step instructions for running **GridViewer** on both Linux and Windows. This guide covers placing the files, linking your ADIF log, starting a local web server, and accessing the tool in your browser.

### 1. Prepare Your Files

- Place `gridviewer.html` in a directory of your choice.
- Ensure your `wsjtx_log.adi` file (your ADIF log) is available.


### 2. Place or Link the Log File

#### **Linux**

- Place `wsjtx_log.adi` in the same directory as `gridviewer.html`.
- Or, if your log is elsewhere, create a symbolic link (recommended):

```bash
ln -s /path/to/your/wsjtx_log.adi /path/to/gridviewer/wsjtx_log.adi
```


#### **Windows**

- Copy `wsjtx_log.adi` into the same folder as `gridviewer.html`.
- Or, create a symlink (requires Command Prompt as Administrator):

```cmd
mklink "C:\path\to\gridviewer\wsjtx_log.adi" "C:\path\to\your\wsjtx_log.adi"
```

(Use full paths and quotes if there are spaces.)


### 3. Start a Local HTTP Server

You need a simple HTTP server so your browser can load the ADIF file. Here are common options:

#### **Using Python (Linux or Windows)**

- **Python 3:**

```bash
cd /path/to/gridviewer
python3 -m http.server 8000
```

- **Python 2:**

```bash
cd /path/to/gridviewer
python -m SimpleHTTPServer 8000
```


#### **Using Node.js (Linux or Windows)** *Not tested by me, but should hopefully work!*

- Install [http-server](https://www.npmjs.com/package/http-server) globally (if not already):

```bash
npm install -g http-server
```

- Start the server:

```bash
cd /path/to/gridviewer
http-server -p 8000
```


#### **Other Options**

- Any static file server will work (e.g., [serve](https://www.npmjs.com/package/serve), [live-server](https://www.npmjs.com/package/live-server), etc.).
- On Windows, you can also use [WSL](https://learn.microsoft.com/en-us/windows/wsl/) to run the Linux instructions.


### 4. Open GridViewer in Your Browser

- Open your web browser.
- Navigate to:

```
http://localhost:8000/gridviewer.html
```

- The tool should load and display your worked grids.    
  
## Notes
- A BAT-file to get GridViewer up and running in one go that has been successful on Windows:
```
@echo off
python -c "__import__('subprocess').Popen(['python', '-m', 'http.server', '8000'], creationflags=0, close_fds=True)" 
start chrome --new-window "http://localhost:8000/gridviewer.html"
```
- You may use any port (e.g., 8000); just match the port in your browser address.
- If your log file updates, simply refresh the browser page.
- No installation is necessary beyond a basic Python or Node.js environment.
