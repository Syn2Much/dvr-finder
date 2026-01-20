
# DVR Scanner & Fingerprinter (Brand Specific)

Fast, multi-threaded scanner that fingerprints surveillance web interfaces (DVR/NVR) and security-related IoT devices. **Strict mode enabled: checks only for specific brands and known signatures.**

![Banner](https://img.shields.io/badge/DVR-Finder-blue)
![Python](https://img.shields.io/badge/Python-3.7%2B-green)
![License](https://img.shields.io/badge/License-MIT-orange)

## Features
- **Brand-Only Detection**: Focuses on major security brands (Hikvision, Dahua, DrayTek, etc.).
- **Zero False Positives**: Removed generic "password" scraping; ignores default Apache/Nginx pages.
- **IoT Support**: Detects security-adjacent IoT devices like DrayTek Vigor, MikroTik, and Ubiquiti.
- **Multi-threaded & Auto-save**: High performance with incremental result saving.

## Installation
```bash
git clone https://github.com/Syn2Much/dvr-finder.git
cd dvr-finder
pip install requests urllib3
```

## Usage
```bash
python dvr_finder -h                     full help
python dvr_finder.py -i ips.txt -t 10 -o dvr_scan_results.json
```


## 📋 Supported Brands
Detection is restricted to verified vendor signatures.

| Category | Brands / Signatures |
|----------|-------------------|
| **DVR / NVR** | **Hikvision**, **Dahua**, **Uniview**, **Samsung/Hanwha**, **Axis**, **Avigilon**, **Mobotix**, **XMEye**, **TVT**, **Amcrest**, **Reolink** |
| **IoT / Routers** | **DrayTek Vigor** (Vigor, Vilet), **MikroTik** (RouterOS), **Ubiquiti** (Unifi, AirOS), **Synology** (Surveillance Station) |

## Disclaimer
**Educational and authorized testing only.** You must have explicit permission to scan networks/devices.
```
