# Look Up — firmware builds

Compiled firmware for the **Look Up** aircraft display, an ESP32-S3 driving a
64×32 HUB75 LED matrix that shows the nearest aircraft overhead.

**Nothing here is written by hand.** Every file is published by the release
workflow in the (private) source repository when a version tag is pushed.

## Why this repo is public

The display checks for updates by fetching the two files below over HTTPS.
Keeping them public means **no credentials are embedded in the device** — it is
a gift living in someone else's house, and there is nothing on it worth
extracting and nothing that can expire.

The source code stays private; only build output is published here.

## Contents

| File | Purpose |
|---|---|
| `manifest.json` | The current release: version, download URL and MD5 |
| `lookup-<version>.bin` | The firmware image itself |

```json
{
  "version": "1.2.0",
  "url": "https://raw.githubusercontent.com/ToastieDesign/lookup-firmware/main/lookup-1.2.0.bin",
  "md5": "…",
  "notes": "v1.2.0"
}
```

The device installs a build only if the version is **strictly newer** than the
one it is running, verifies the MD5 as it downloads, and refuses any URL that
is not HTTPS on `githubusercontent.com`.

## If you found this by accident

There is nothing to run here — these are ESP32-S3 binaries for one specific
hand-built device. Flashing one to other hardware will not do anything useful.

## Safety

The display writes each update into a spare flash slot and must confirm itself
after rebooting. If a build fails to start, the bootloader automatically
reverts to the previous one, so a bad release cannot leave the device dead.

Deleting this repository does not break any display already in the field — it
simply stops receiving updates and carries on working as before.
