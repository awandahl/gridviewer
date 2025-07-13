# <img width="400" height="400" alt="gridviewer" src="https://github.com/user-attachments/assets/0f881a14-4194-4a82-a71d-8203ef1d028e" />
![gridviewer](https://github.com/user-attachments/assets/7608478f-992a-45c9-9c9d-0fd4b1a2dd04)


## How to Use GridViewer on Linux and Windows

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


## Quick Reference Table

| Step | Linux Command/Action | Windows Command/Action |
| :-- | :-- | :-- |
| Place files | Put both files in same directory | Same |
| Symlink log file | `ln -s /path/to/wsjtx_log.adi ./wsjtx_log.adi` | `mklink` (see above) |
| Start server (Python) | `python3 -m http.server 8000` | `python -m http.server 8000` |
| Start server (Node) | `http-server -p 8000` | `http-server -p 8000` |
| Open in browser | `http://localhost:8000/gridviewer.html` | Same |

## Notes

- You may use any port (e.g., 8000); just match the port in your browser address.
- If your log file updates, simply refresh the browser page.
- No installation is necessary beyond a basic Python or Node.js environment.
