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
