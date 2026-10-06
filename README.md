<div align="center">

<img src="appicon-remove-back.png" alt="vBook Link Icon" width="128" height="128" />

# vBook Link

**A lightweight, local-first OPDS and WebDAV catalog server for the vBook reading ecosystem on Android.**

[![Release](https://img.shields.io/badge/Release-v1.2.0-blue.svg)](https://github.com/kychitoge/vbook-link-app/releases)
[![Android](https://img.shields.io/badge/Android-8.0%2B%20(API%2026%2B)-green.svg)](https://developer.android.com)
[![Architecture](https://img.shields.io/badge/Architecture-Local--First%20%7C%20Zero--Cloud-orange.svg)](#architecture-and-privacy)
[![License](https://img.shields.io/badge/License-MIT-purple.svg)](LICENSE)

</div>

---

## Overview

**vBook Link** runs as a companion background server directly on your Android device. It indexes your Google Drive book collections and generates standard Atom XML OPDS 1.2 and WebDAV feeds. 

By delivering feeds locally over the loopback network (`127.0.0.1`), vBook Link lets you browse and download books directly into the **vBook** reading app with maximum speed, zero hosting costs, and complete privacy.

---

## Key Features

- **Standard OPDS 1.2 & WebDAV Support**: Seamlessly integrates with vBook and any standard OPDS/WebDAV reader client.
- **Full Format Detection**: Automatically recognizes 13 major ebook formats, including `.epub`, `.pdf`, `.cbz`, `.cbr`, `.mobi`, `.prc`, `.azw`, `.azw3`, `.fb2`, `.docx`, `.doc`, `.zip`, and `.txt`.
- **Native Vector Covers**: Extracts file categories to render sharp SVG vector covers in vBook, reducing XML payload size by 35% without downloading external thumbnails.
- **Direct Google CDN Downloads**: Directs file downloads straight from Google's high-speed CDN (`HTTP 302 Found`). Books stream directly to your reader without wasting mobile device RAM or relay bandwidth.
- **On-Demand Hierarchical VFS**: Loads folders instantly without deep-scan delays. Browse large directory structures smoothly with sub-second response times.
- **Reliable Foreground Service**: Keeps the local Ktor server active while you read in vBook, preventing background process termination by the operating system.
- **Private by Design (BYOK)**: Supports Bring Your Own Key for Google Drive access. Your keys and catalog data remain strictly on your local device.
- **Backup and Device Transfer**: Easily back up and restore your catalog sources and preferences using standard open JSON files. Move your library to new phones or E-ink devices in seconds with zero cloud intermediaries.

---

## Prerequisites

Before installing vBook Link, verify that your environment meets the following requirements:

- **Operating System**: Android 8.0 (API Level 26, Oreo) or higher.
- **Target Reader**: [vBook](https://github.com/kychitoge) or any reading application with OPDS support.
- **Network Access**: Local Wi-Fi connection (for multi-device LAN access) or internal loopback interface (for on-device reading).

---

## Get Started

Follow these steps to set up and connect vBook Link to your reading application.

### Step 1: Install the application
1. Go to the [Releases](https://github.com/kychitoge/vbook-link-app/releases) page.
2. Download the latest `vBookLink-v1.2.0-release.apk` package.
3. Open the downloaded file on your Android device and confirm installation.

### Step 2: Start the local server
1. Open **vBook Link**.
2. Tap the **Power** button on the home screen to start the server.
3. Verify that the server status indicates **Running**.
4. Tap the **OPDS** URL card to copy the local catalog link (default: `http://127.0.0.1:8686/opds`).

### Step 3: Add your book sources
You can connect Google Drive collections using either of the following methods:
- **Direct Link**: In the **Files** tab, tap **(+)**, paste your public or shared Google Drive folder link, and select **Add**.
- **System Share Menu**: Open Google Drive or your browser, choose **Share Link**, and select **vBook Link** from the application sheet.

### Step 4: Connect with vBook
1. Open the **vBook** reading application.
2. Navigate to **OPDS Bookshelf** > **Add Catalog**.
3. Enter a title (for example, `My Local Library`) and paste the copied URL (`http://127.0.0.1:8686/opds`).
4. Save the entry, open your catalog, and select any title to download and read.

---

## Architecture and Privacy

vBook Link is engineered with a strict **Local-First** design:

```
[Google Drive CDN] <================== (Direct Download HTTP 302) ================== [vBook Reader]
         ^                                                                                    |
         | (Metadata Query)                                                                   | (OPDS Feed)
         v                                                                                    v
  [vBook Link App] ------------------- (127.0.0.1 / Local LAN) --------------------> [Local Server]
```

- **Zero Cloud Intermediaries**: All catalog indexing and HTTP serving occur strictly on your hardware.
- **No Analytics or Trackers**: The application contains no telemetry, advertisement SDKs, or remote reporting.
- **Secure Credentials**: All API credentials and cached metadata are stored exclusively in private application storage (`Room SQLite` / `Encrypted Preferences`).

---

## Technical Specifications

| Parameter | Specification |
|---|---|
| **Package Name** | `com.vbook.link` |
| **Minimum Android Version** | Android 8.0 (API 26) |
| **Target Android Version** | Android 14 (API 34) |
| **Engine Framework** | Kotlin 2.0 / Jetpack Compose / Ktor CIO 2.3.12 |
| **Default Server Port** | `8686` (Configurable in Settings) |
| **Signature Schemes** | APK Signature Scheme v1, v2, and v3 |

---

## Troubleshooting

### Play Protect Warning ("Unrecognized Developer")
- **Cause**: vBook Link is distributed directly via sideloading rather than the Google Play Store, so new signing certificates initially lack community reputation in Google's database.
- **Solution**: Select **More details** > **Install anyway**. The official release is cryptographically signed and verified.

### Server Connection Failed
- If vBook displays a connection timeout error, ensure that:
  1. The server switch inside vBook Link is turned **ON**.
  2. The address is entered exactly as shown on the home screen (`http://127.0.0.1:8686/opds`).
  3. If another service occupies port 8686, vBook Link automatically triggers auto-recovery port fallback (+1, +2). You can also open **Settings** inside vBook Link and assign an alternate port manually.

---

## License and Copyright

Copyright (c) 2026 **kychitoge**. All rights reserved.

Distributed under the terms of the [MIT License](LICENSE).
