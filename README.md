# Torrent Downloader & FTP Server Stack

This repository provides a Docker Compose stack configured for GitHub Codespaces / Linux VM that runs:
1. **qBittorrent** (Web UI accessible at `http://localhost:8080`)
2. **Alpine vsftpd FTP Server** (Accessible at port `21` and passive data ports `21000-21005`)

Both services share the `./downloads` directory, allowing you to download torrents directly in Codespaces and transfer them to your local laptop over FTP.

---

## Quick Start

### 1. Start the stack
```bash
docker compose up -d
```

### 2. Check running status
```bash
docker compose ps
docker compose logs -f
```

### 3. Stop the stack
```bash
docker compose down
```

---

## Accessing the Services from your Laptop

### 🌐 qBittorrent Web UI
* **URL:** [http://localhost:8080](http://localhost:8080)
* **Default Port:** `8080` (Automatically forwarded by Codespaces to your laptop's localhost)
* **Login:** Pre-configured with local subnet bypass (instant access). If prompted, default username is `admin`. You can set a custom WebUI password anytime in **Tools -> Options -> Web UI**.

---

### 📁 FTP Server
Connect using any FTP client on your laptop (e.g. FileZilla, WinSCP, Cyberduck):

* **Host / Server:** `127.0.0.1` or `localhost`
* **Port:** `21`
* **Protocol:** FTP (Plain FTP)
* **Transfer Mode:** Passive
* **Username:** `admin` *(configured in `.env`)*
* **Password:** `admin123` *(configured in `.env`)*

> **Codespaces Port Forwarding Note:**  
> Codespaces forwards port `8080` (Web UI) and port `21` (FTP control).  
> For data transfers over FTP, passive ports `21000-21005` are also mapped. Ensure ports `21` and `21000-21005` appear in the VS Code **Ports** tab (forwarded to `localhost`).

---

## Configuration (`.env`)

You can customize credentials and ports in the [.env](file:///workspaces/t2d/.env) file:

```env
PUID=1000
PGID=1000
TZ=Etc/UTC

WEBUI_PORT=8080
TORRENTING_PORT=6881

FTP_USER=admin
FTP_PASS=admin123
FTP_PORT=21
FTP_PASV_ADDRESS=127.0.0.1
FTP_PASV_MIN_PORT=21000
FTP_PASV_MAX_PORT=21005
```
