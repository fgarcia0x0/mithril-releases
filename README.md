# Mithril releases

Downloads and update manifests for **Mithril**, a serverless peer-to-peer voice and text room (text on a DataChannel, voice and screen sharing over WebRTC, no server of ours anywhere).

This repository only carries releases. The source code is not published here.

## Download

Get the newest version from the [latest release](../../releases/latest).

| File | What it is |
|---|---|
| `mithril-windows-x64.msix` | Windows installer, signed with a self-signed development certificate |
| `mithril-dev-cert.cer` | The public certificate that signed the MSIX: import it before installing |
| `mithril-windows-msvc-x64.zip` | Windows portable build: unzip and run `mithril.exe` |
| `mithril-linux-x86_64.AppImage` | Linux x86_64: `chmod +x` it and run |
| `SHA256SUMS.txt` | Checksums of the files above: compare them before installing |

Releases named `vX.Y.Z-dev.N` are pre-releases from the development channel.

### Installing the MSIX on Windows
Run PowerShell as Administrator in the folder with the files:

```powershell
Import-Certificate -FilePath "mithril-dev-cert.cer" -CertStoreLocation "Cert:\LocalMachine\TrustedPeople"
Add-AppxPackage -Path "mithril-windows-x64.msix"
```

The certificate is self-signed and only trusted for packages signed with it.

## For the in-app updater

Mithril checks for updates by reading one small file per channel:

- `https://github.com/fgarcia0x0/mithril-releases/releases/download/channel-stable/version.json`
- `https://github.com/fgarcia0x0/mithril-releases/releases/download/channel-dev/version.json`

`channel-stable` and `channel-dev` are pointer releases (marked as pre-releases so they never become "latest"). Each holds a single `version.json`, replaced on every publication; there are no binaries to download from them. The manifest names the files, and their SHA-256, of the version the channel currently points to.
