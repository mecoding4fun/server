# 🚀 Secure Cloud Storage Server + Web UI + Flutter Mobile Client

A self-hosted personal cloud system built using **FastAPI** and **React UI**. This system allows you to upload, download, preview files, stream videos, and manage folders remotely.

> 💡 **Concept:** Works like a mini Google Drive that you control yourself. Ideal for private home-server usage.


## ✨ Features

* **📁 Remote File Explorer:** UI for both Mobile & Web.
* **🔑 Secure:** API-Key protected backend.
* **🖼 Media Ready:** Image preview with loading spinners.
* **🎬 Video Streaming:** Real chunked streaming via FastAPI (not full downloads).
* **📤 Uploads:** Support for Camera, Gallery, and File Picker (Multi-upload supported).
* **📥 Downloads:** Saves files directly to the device's actual Downloads folder.
* **📂 Management:** Create folders and delete files.
* **⚡ Network:** Optimized for Global access.

## 🏗 Tech Stack

| Layer | Technology |
| :--- | :--- |
| **Backend** | FastAPI (Python) |
| **Mobile Client** | Flutter |
| **Storage** | Local filesystem |
| **Streaming** | FastAPI chunked video |
| **Network** | Cloudflare tunnel |


## 🔧 Server Setup (Backend)

1.  Navigate to the server directory and set up the environment:
    ```bash
    cd server
    python3 -m venv venv
    source venv/bin/activate  # On Windows use: venv\Scripts\activate
    pip install -r requirements.txt
    ```

2.  **Configuration:**
    Open `server.py` and update the following configuration:
    ```python
    API_KEY = "SETAPIKEY"   # Change this to a secure key
    SHARED_DIR = "shared"     # Storage directory
    ```

3.  Run the server:
    ```bash
    uvicorn server:app --host 0.0.0.0 --port 8000
    ```

## 📱 Flutter App Setup (Mobile Client)

1.  Navigate to the app directory:
    ```bash
    cd mobile_client/remote_file_client
    flutter pub get
    ```

2.  **Configuration:**
    Open `lib/main.dart` and update the connection details:
    ```dart
    // Use your Tailscale IP here (starts with 100.x.x.x)
    final String baseUrl = "http://YOUR_TAILSCALE_IP:8000"; 
    
    // Must match the key in server.py
    final String apiKey  = "changeme123"; 
    ```

3.  **Android Manifest Config:**
    To allow video streaming over HTTP, you must allow cleartext traffic.
    Open `android/app/src/main/AndroidManifest.xml` and add the `usesCleartextTraffic` line:
    ```xml
    <application
        android:label="Remote File Client"
        android:name="${applicationName}"
        android:icon="@mipmap/ic_launcher"
        android:usesCleartextTraffic="true"> ...
    </application>
    ```

4.  Run the app:
    ```bash
    flutter run
    ```
## 🌐 Web Client Setup (Optional Web UI)

> The Web Client lets you access files from any browser, similar to a lightweight cloud drive interface.

### 📁 Requirements

- Node.js & npm installed
- Backend FastAPI server running
- Same Tailscale network (unless you expose server publicly)

---

### 🚀 Setup & Run

```bash
cd web_client        # enter web client folder
npm install          # install dependencies
npm run dev          # start development server

## 🔐 Access Flow

1.  Start the **FastAPI server** on your host machine.
2.  Get the **Tailscale IP** from the server device.
3.  Enter the IP + API Key inside the App configuration.
4.  Browse, upload, and stream files remotely.

**Example URL:** `http://100.xxx.xxx.xxx:8000`

## 🔮 Future Enhancements

* [ ] User accounts + Authentication system
* [ ] Shareable public links

## 👤 Credits

Built by **Ramachandran**.
Originally configured to operate over **Tailscale private VPN**.
