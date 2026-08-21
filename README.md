# m7300_bundle

Bundles the [pantum_m7300](https://github.com/DrAbcOfficial/pantum_m7300) drivers and the [m7300_scan_gui](https://github.com/DrAbcOfficial/m7300_scan_gui) scanner app into Debian packages, built and published automatically by GitHub Actions.

## Build

- **Runner:** `ubuntu-24.04-arm` (ARM64)
- **Trigger:** push a tag `v*` or run the workflow manually (`workflow_dispatch`)
- **Version:** read from the `VERSION` file in this repo (currently `1.0.1`). Tag-triggered builds require the tag to match it exactly (e.g. tag `v1.0.1`). To release a new version: bump `VERSION`, commit, tag, push.

Both variants are built in parallel:

| Variant | Package | eSCL/airscan | PNG/JPEG |
|---|---|---|---|
| full | `pantum-m7300-bundle` | ON (depends on `sane-airscan`) | ON |
| noairscan | `pantum-m7300-bundle-noairscan` | OFF | ON |

## Artifacts

Published as GitHub Release assets for each tag:

- `pantum-m7300-bundle_<version>_arm64.deb`
- `pantum-m7300-bundle-noairscan_<version>_arm64.deb`
- matching `.sha256` checksum files

Each package contains: CUPS printer drivers (filters + PPDs), SANE scanner backends (`m7300fdn`, `m7300fdw`, auto-registered in `dll.conf`), scan CLI utilities, and the `pantum-scan-gui` desktop app.

## Install

```bash
# pick one variant
sudo apt install ./pantum-m7300-bundle_1.0.1_arm64.deb
# or
sudo apt install ./pantum-m7300-bundle-noairscan_1.0.1_arm64.deb
```

Requires Ubuntu/Debian on ARM64 with `libsane1`, `libcups2` and `libwebkit2gtk-4.0-37` (or `4.1`); dependencies are resolved automatically by `apt`. After installation, launch **Pantum Scanner** from the applications menu or run `pantum-scan-gui`.
