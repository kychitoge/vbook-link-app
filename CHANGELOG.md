# Changelog

All notable changes to the vBook Link project are documented in this file. This project follows [Semantic Versioning 2.0.0](https://semver.org/).

---

## Version 1.2.0 (2026-10-06)

This release introduces native backup and restore capabilities, allowing you to seamlessly transfer your book sources and settings between devices with complete privacy and zero cloud dependencies.

### What's new

- **Library backup and restore**: Back up your book catalog sources and server settings to a lightweight, standard open JSON file.
- **Easy device migration**: Transfer your library from an old phone to a new smartphone, tablet, or E-ink reading device (Boox, Meebook) in seconds.
- **Direct file sharing**: Share backup files directly from the app using Android Quick Share, Google Drive, Bluetooth, or messaging apps.
- **Dedicated management screen**: Access all backup and restore actions from a clean, card-based interface in **Settings** > **Đồng bộ & sao lưu**.
- **Flexible restore options**: Choose between merging with existing catalog sources or completely replacing your library.

### Improvements

- **Minimal application footprint**: Advanced R8 dead-code elimination and resource shrinking keep the release package at just **3.34 MB**, adding only 18 KB for the entire new feature set.
- **Dynamic version reporting**: Settings now dynamically reads the exact installed application version directly from the operating system.
- **Enhanced navigation experience**: Added native Android back-handler support so you can return to Settings using standard system back gestures without accidentally closing the application.
- **Defensive data validation**: Automatic trimming and filtering prevent invalid or malformed data from corrupting your local database.

### Security and privacy

- **Selective credential export**: Choose whether to include your personal Google Drive API Key when creating a backup file.
- **Zero cloud telemetry**: All backup and restore actions occur strictly on your local hardware through Android Storage Access Framework (SAF).

---

## Version 1.1.0 (2026-10-02)

This release introduced Bring Your Own Key (BYOK) architecture, on-demand hierarchical virtual file systems, and multi-scheme release signing.

### What's new

- **Bring Your Own Key (BYOK)**: Connect Google Drive folders using your own API key to ensure privacy and eliminate community quota bottlenecks.
- **On-demand hierarchical VFS**: Browse nested folder structures smoothly with sub-second response times without deep-scan delays.
- **Auto-recovery port fallback**: Server automatically detects port conflicts (such as port 8080) and shifts smoothly to port 8686.

### Security and privacy

- **Release keystore signing**: Signed using RSA 4096-bit certificates supporting APK Signature Schemes v1, v2, and v3 to resolve Play Protect warnings.
- **Credential sanitization**: System logs automatically redact sensitive API keys.

---

## Version 1.0.0 (2026-09-18)

- Initial release of vBook Link with embedded Ktor CIO server, OPDS 1.2 catalog feeds, and WebDAV support.
