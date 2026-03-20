# VRS X — Virtual Radar Server X

ADS-B receiver and aircraft tracking server. Displays live aircraft on an interactive map using data from your SDR receiver.

---

## Download

Go to [Releases](../../releases/latest) and download the archive for your platform:

| File | Platform |
|---|---|
| `osx-arm64.zip` | macOS (Apple Silicon) |
| `linux-x64.zip` | Linux (64-bit Intel/AMD) |
| `linux-arm64.zip` | Linux (ARM64 — Raspberry Pi 4/5, etc.) |
| `win-x64.zip` | Windows (64-bit) |

---

## Running

### macOS

1. Download and unzip `osx-arm64.zip`
2. Double-click **VRSX.app**
3. Open your browser at `http://localhost:8080`
4. Admin panel: `http://localhost:5000/admin`

> On first launch macOS may block the app. Go to **System Settings → Privacy & Security** and click **Open Anyway**.

---

### Windows

1. Download and unzip `win-x64.zip`
2. Run **VirtualRadar.Desktop.exe**
3. Open your browser at `http://localhost:8080`
4. Admin panel: `http://localhost:5000/admin`

---

### Linux

1. Download and unzip the appropriate archive:

```bash
unzip linux-arm64.zip
cd linux-arm64
chmod +x VirtualRadar.Desktop
./VirtualRadar.Desktop --headless
```

2. Open your browser at `http://<server-ip>:8080`
3. Admin panel: `http://<server-ip>:5000/admin`

#### Run as a systemd service (recommended)

Create the service file:

```bash
sudo nano /etc/systemd/system/vrsx.service
```

Paste the following (adjust `User`, `WorkingDirectory` and `ExecStart` to match your setup):

```ini
[Unit]
Description=VRS X — Virtual Radar Server
After=network.target

[Service]
Type=simple
User=YOUR_USER
WorkingDirectory=/home/YOUR_USER/linux-arm64
ExecStart=/home/YOUR_USER/linux-arm64/VirtualRadar.Desktop --headless
Restart=on-failure
RestartSec=5

[Install]
WantedBy=multi-user.target
```

Enable and start:

```bash
sudo systemctl daemon-reload
sudo systemctl enable vrsx
sudo systemctl start vrsx
```

Check status:

```bash
sudo systemctl status vrsx
```

---

## Updating

> Your data and settings are stored separately from the application files and are preserved across updates.

### macOS / Windows

1. Stop the application
2. Download the new release and unzip it
3. Overwrite the existing files with the new ones
4. Start the application

### Linux — systemd

```bash
sudo systemctl stop vrsx
# download and unzip the new release into the same directory, overwriting files
sudo systemctl start vrsx
```

### Linux — terminal / desktop

1. Stop the running process (`Ctrl+C` or close the window)
2. Download and unzip the new release, overwriting the existing files
3. Start the application again

---

## Known Issues

**Admin panel window does not open / appears blank**

If the admin panel window fails to open or is unresponsive, navigate directly to:

```
http://localhost:5000/admin
```

Opening it in the browser first will cause the embedded window to work correctly afterwards. This is a known issue that will be addressed in a future release.

---

## Data Directory

VRS X stores all configuration, database and logs in a platform-specific directory:

| Platform | Path |
|---|---|
| macOS | `~/Library/Application Support/VRSX/` |
| Linux | `~/.vrsx/` |
| Windows | `%APPDATA%\VRSX\` |

You can override this by setting the `VRS_DATA_DIR` environment variable.
