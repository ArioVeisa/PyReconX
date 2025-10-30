# PyReconX

> ⚡ Automated Reconnaissance & Vulnerability Discovery Toolkit — **Python-based, offline-capable, modular.**
> **Status:** 🚧 **COMING SOON** — initial public release under development.

[![Status](https://img.shields.io/badge/status-coming%20soon-orange.svg)](#)
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](#)
[![Python](https://img.shields.io/badge/python-3.10%2B-green.svg)](#)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](#)

---

## 🔥 What is PyReconX?

**PyReconX** is a CLI tool for automated **reconnaissance and vulnerability discovery**.
It’s designed to be **lightweight**, **modular**, and **fully offline-capable** — built for pentesters, CSIRT analysts, security researchers, and developers.

Key strengths:

* Works **without API dependencies**.
* Modular design (Recon, Alive Check, Port Scan, Vuln Templates).
* **Fast** (asyncio engine) and **lightweight**.
* Outputs **HTML & JSON reports** ready for documentation.

---

## ✨ Key Features

* Subdomain enumeration (brute-force + DNS resolver).
* Alive host checker (HTTP/HTTPS async verification).
* Asynchronous port scanning (top/common ports).
* Vulnerability scanning via **YAML-based templates** (XSS, SQLi, LFI, Misconfigurations, etc.).
* Report generator (HTML & JSON summary).
* Optional alert system (Telegram/Webhook).
* **Auto resource downloader** (wordlists + templates fetched on first run).

---

## 🧱 Architecture Overview

```
PyReconX (CLI)
   └─ Async Task Orchestrator
       ├─ Recon        → subdomains.txt
       ├─ Web Check    → alive.txt
       ├─ Port Scan    → open_ports.json
       ├─ Vuln Scanner → vuln_results.json
       └─ Report Gen   → report.html / summary.json
```

---

## 📦 Installation (COMING SOON)

> PyPI distribution is being prepared. For now, use local mode.

```bash
# 1) Clone the repo
git clone https://github.com/<username>/PyReconX.git
cd PyReconX

# 2) Create virtual environment (recommended)
python3 -m venv .venv && source .venv/bin/activate

# 3) Install dependencies
pip install -r requirements.txt

# 4) First run (auto downloads resources)
python -m pyreconx --help
```

> Future release:

```bash
pip install pyreconx
pyreconx --help
```

---

## 🚀 Quick Start Example

```bash
# Full scan (Recon → Alive → Ports → Vuln → Report)
python -m pyreconx --domain target.com --fullscan

# Individual modules
python -m pyreconx --domain target.com --recon
python -m pyreconx --domain target.com --alive
python -m pyreconx --domain target.com --ports
python -m pyreconx --domain target.com --vuln --templates data/templates/
```

**Output Directory Example:**

```
/output/target.com/
 ├── subdomains.txt
 ├── alive.txt
 ├── open_ports.json
 ├── vuln_results.json
 └── report.html
```

---

## ⚙️ CLI Options

```text
--domain <str>        Target domain
--fullscan            Run all modules sequentially
--recon               Run subdomain enumeration only
--alive               Run alive check only
--ports               Run port scan only
--vuln                Run vulnerability scan only
--templates <path>    Path to YAML templates
--threads <int>       Concurrency (default: 100)
--timeout <int>       Timeout per request (seconds)
--update              Update resources (wordlists/templates)
--out <path>          Custom output directory
--silent              Minimal logging
```

---

## 🧪 Example Output

```
[+] Enumerating subdomains...
[✓] Found 52 subdomains
[+] Checking live hosts...
[✓] 18 alive
[+] Scanning ports...
[✓] Open ports found on 7 hosts
[+] Running vulnerability templates...
[!] 2 HIGH, 1 MEDIUM
[+] Report saved: output/target.com/report.html
```

**Report (Mockup Preview)**

```
PyReconX Report – target.com (2025-10-30)
Summary:
  Subdomains: 52 | Alive: 18 | Open Ports: 8
  Vulnerabilities: 3 (2 High, 1 Medium)

Vulnerabilities:
  https://api.target.com     SQL Injection     HIGH
  https://cdn.target.com     Reflected XSS     MEDIUM
  https://admin.target.com   Exposed Panel     HIGH

Port Summary:
  api.target.com → 80, 443, 8080
  db.target.com  → 3306
```

> 📷 Screenshot placeholder: `docs/report-preview.png` *(COMING SOON)*

---

## 🗂️ Project Structure

```
pyreconx/
 ├─ __init__.py
 ├─ main.py                # CLI entry
 ├─ core/
 │   ├─ recon.py           # subdomain enumeration
 │   ├─ webcheck.py        # alive checker
 │   ├─ portscan.py        # async TCP scanner
 │   ├─ vulnscan.py        # YAML vulnerability templates
 │   └─ report.py          # HTML/JSON report generator
 ├─ data/
 │   ├─ templates/         # vulnerability templates
 │   └─ wordlists/         # subdomain lists
 └─ installer.py           # resource auto-downloader
```

---

## 🧩 YAML Vulnerability Template Example

```yaml
id: xss-basic
info:
  name: Reflected XSS (Basic)
  severity: medium
requests:
  - method: GET
    path:
      - "{{BaseURL}}/?q=<script>alert(1)</script>"
    matchers:
      - type: word
        words:
          - "<script>alert(1)</script>"
```

Save your custom templates under `data/templates/`.

---

## 🔄 Updating Resources

```bash
python -m pyreconx --update
```

Automatically pulls the latest **wordlists** and **vulnerability templates** from the remote resource repository (COMING SOON).

---

## 🗺️ Development Roadmap

* [x] CLI skeleton
* [x] Core modules: Recon / Alive / Ports / Vuln / Report
* [ ] Auto-update resources
* [ ] Telegram/Webhook notifier
* [ ] CVSS auto scoring
* [ ] Dashboard (FastAPI + Tailwind)
* [ ] PyPI release (`pip install pyreconx`)

---

## 🤝 Contributing

1. Fork this repo & create a new branch.
2. Follow PEP8 style guidelines.
3. Add tests/examples for new features.
4. Submit a PR with a brief description.

We welcome contributions from the community!

---

## 🛡️ Disclaimer

This project is intended for **educational and authorized security testing only**.
Use PyReconX **only on systems you own or have explicit permission to test**.
The author assumes **no liability** for misuse or illegal activity.

---

## 📄 License

Licensed under the **MIT License** — free for modification and distribution with proper attribution.

---

## 📫 Contact

* Author: **Ario Veisa Rayanda Utomo**
* Project: **PyReconX – Automated Recon & Vulnerability Discovery**
* Status: 🚧 *Coming soon – early access planned Q4 2025*

---

### 🏁 Release Notes

* **v0.1.0 (COMING SOON):** Public MVP release (CLI + templates + HTML report).
* **v0.2.x:** Notifier + auto-update resources.
* **v0.3.x:** Dashboard API + PyPI package.
