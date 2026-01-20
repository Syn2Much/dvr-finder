

# DVR Scanner & Fingerprinter (Strict Mode)

Fast, multi-threaded DVR/NVR scanner that fingerprints common surveillance web interfaces from a list of IPs. **Now optimized for strict detection to eliminate false positives.**

![Banner](https://img.shields.io/badge/DVR-Finder-blue)
![Python](https://img.shields.io/badge/Python-3.7%2B-green)
![License](https://img.shields.io/badge/License-MIT-orange)
![Threading](https://img.shields.io/badge/Multi--Threaded-Yes-brightgreen)

## Features
- **Strict Login Detection**: Targets specific login pages (`login.cgi`, `doc/page/login.asp`) and authentic brands.
- **False Positive Elimination**: Ignores generic "camera" or "security" terms unless they appear in a verified login context (e.g., `<title>` tags or login forms with `user`/`pass` fields).
- **Multi-threaded scanning**: High-performance thread pool execution.
- **Auto-save**: Saves results incrementally while scanning + **Ctrl+C** graceful save/exit.
- **Resilient**: Handles timeouts, SSL errors, and encoding fallbacks automatically.

## Installation
```bash
git clone https://github.com/Syn2Much/dvr-finder.git
cd dvr-finder
pip install -r requirements.txt
```

Or manually install dependencies:
```bash
pip install requests urllib3
```

**Requirements:** Python 3.7+

## Usage
```bash
python dvr_finder.py -i ips.txt -t 10 -o dvr_scan_results.json
```

Common options:
- `-i, --input` IP list (default: `ips.txt`)
- `-t, --threads` threads (default: `10`)
- `--save-interval` save every N DVRs found (default: `10`)
- `-o, --output` output JSON (default: `dvr_scan_results.json`)
- `-v, --verbose` verbose output

Examples:
```bash
python dvr_finder.py
python dvr_finder.py -t 20
python dvr_finder.py -i my_ips.txt -t 30 -v
python dvr_finder.py --save-interval 5
```

## Input / Output
**Input:** one IP per line.
```txt
192.168.1.1
192.168.1.2
10.0.0.1
```

**Outputs:**
- `dvr_scan_results.json` — full fingerprint details per hit
- `dvr_ips.txt` — plain list of DVR IPs found

## 📋 Supported DVR Brands
*Detection is now restricted to specific signatures and valid login portals.*

| Brand | Detection Patterns (Partial) |
|-------|-------------------|
| **Hikvision** | `doc/page/login.asp`, `ivms`, `webcomponent`, `hikvision` |
| **Dahua** | `login.cgi`, `guilogin.cgi`, `dss-web`, `dahuasecurity` |
| **Uniview** | `/LAPI/V1.0`, `program/login`, `uniarch` |
| **Samsung/Hanwha** | `wisenet`, `hanwha`, `samsung techwin` |
| **Axis** | `axis communications`, `axis network camera` |
| **Avigilon** | `avigilon` |
| **Mobotix** | `mobotix` |
| **XMEye** | `xmeye`, `cloud.net` |
| **Generic Login** | Verified login forms containing keywords like `onvif`, `rtsp`, `stream` |


## Example Output
```
    ╔═══════════════════════════════════════════════════════════════════════════════╗
    ║    ____________   ______________  ___________.__            . ___              ║
    ║    \______ \   \ /   /\______   \ \_   _____/|__| ____    __| _/___________   ║
    ║    |    |  \   Y   /  |       _/  |    __)  |  |/    \  / __ |/ __ \_  __ \   ║
    ║    |    `   \     /   |    |   \  |     \   |  |   |  \/ /_/ \  ___/|  | \/   ║
    ║    /_______  /\___/    |____|_  /  \___  /   |__|___|  /\____ |\___  >__|     ║
    ║            \/                 \/       \/            \/      \/    \/         ║
    ║                         DVR Scanner & Fingerprinter                           ║
    ║                         v2.0 - dev@sinners.cty                                ║
    ╚═══════════════════════════════════════════════════════════════════════════════╝    

                     🔍 Scanning for DVR Devices

                     💡 Press Ctrl+C to save and exit gracefully

════════════════════════════════════════════════════════════════════════
Starting DVR Scanner on ips.txt with 10 threads...
════════════════════════════════════════════════════════════════════════

✓ [1/1000] 192.168.1.1 - Status: 200 (not DVR)
✗ [2/1000] 192.168.1.2 - Connection refused
🎯 [3/1000] DVR FOUND: 192.168.1.100 | Status: 200 | Type: Hikvision
🎯 [4/1000] DVR FOUND: 10.0.0.55 | Status: 200 | Type: Generic Login (Context: Login page with 'stream')
...
💾 Auto-saved 10 DVR results
...
```

## Adding signatures
Add new patterns to the `dvr_signatures` dictionary inside `detect_dvr_type_with_signatures()`.

## Disclaimer
**Educational and authorized testing only.** You must have explicit permission to scan networks/devices. The authors are not responsible for misuse or damage.
