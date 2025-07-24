![gt_0 8h_screeshot](https://github.com/user-attachments/assets/aec7ca60-bd83-4831-a32e-7a89412bebae)


## What GridViewer Can Do

**GridViewer** is an interactive and lightweight open source web-based tool designed for ham radio operators to visualize and analyze their worked grid squares from log files. **GridViewer** was developed to address a real-world challenge faced by many ham radio operators using lightweight or single-board computers like the Rock 4 SE (in my case) or Raspberry Pi. Special thanks to Jeffrey B. Otterson, N1KDO, whose grid mapping logic and open-source code https://github.com/n1kdo/lotw-gridmapper provided crucial inspiration and a foundation for this tool.

[**Installation Instructions**](https://github.com/awandahl/gridviewer/blob/main/Installation.md)

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

## Why GridViewer Was Created

**GridViewer** was developed to address a real-world challenge faced by many ham radio operators using lightweight or single-board computers like the Rock 4 SE (in my case) or Raspberry Pi:

- **Resource Efficiency:** Popular programs like GridTracker, while feature-rich and beloved by many, are quite large (around 200MB) and can be resource-intensive. On low-power devices, running both WSJT-X and GridTracker simultaneously can overwhelm the system, resulting in sluggish performance or even making it impossible to operate both at once.
- **Lightweight Alternative:** GridViewer was designed to be a minimal, efficient, browser-based solution for visualizing worked grid squares. It requires only a web browser, a small HTML file, and your log file—making it ideal for systems with limited CPU and memory.
- **Practical Motivation:** The need for a tool that could run smoothly alongside WSJT-X on a device like the Rock 4 SE was the direct inspiration for GridViewer. By focusing on essential features and avoiding heavy dependencies, GridViewer enables real-time grid mapping without taxing the system.


### Key Advantages of GridViewer

- **Tiny Footprint:** Runs in any modern browser, no installation or large packages required.
- **Low CPU Usage:** Minimal background processing, making it suitable for low-power hardware.
- **Simple Setup:** Just serve the HTML file and your log—no complex configuration or dependencies.
- **Responsive:** Allows you to run WSJT-X and GridViewer together even on modest hardware.


  Good luck!
  Anders SM0HPL

