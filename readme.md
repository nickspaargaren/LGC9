## LG OLED webOS 4 – Root HOWTO

## Prerequisites

- **Web/TV:** Create developer account at https://webostv.developer.lge.com (same region as tv) an log in with this account on tv
- **macOS/Linux tools:**
  - `nodejs`
  - `npm`

## Install Developer mode app on TV

On the TV, open content store, install the **Developer Mode** app. Open app, login (again) with developer account created in step 1.

- Enable **Developer Mode** (Reboot after as suggested)
- Enable the **Key Server**

## Install webOS CLI

```bash
npm install -g @webos-tools/cli
```

Verify if it's intstalled:

```bash
ares -V
```

## Configure the device in webOS CLI

Then add the TV as a device:

```bash
ares-setup-device
```

Fetch basic device info:

```bash
ares-device -i --device LGC9
```

## Sanity checks with ares-novacom

Run a simple command on the TV:

```bash
ares-novacom --device LGC9 --run "ls"
```

Example output:

```text
jail_app.conf
jail_app.conf.sig
log
temp
```

## Rooting with faultmanager-autoroot

Run the autoroot script via `ares-novacom`:

```bash
ares-novacom --device LGC9 --run "curl -L -o /tmp/autoroot.sh -- 'https://raw.githubusercontent.com/throwaway96/faultmanager-autoroot/refs/heads/main/autoroot.sh' && sh /tmp/autoroot.sh"
```

Example log excerpts:

```text
...
[ ] Installing /tmp/autoroot.f2k6KL/hbchannel.ipk...
[ ] Homebrew Channel has been elevated
[ ] Current firmware verifies start-devmode.sh signature
[ ] Your start-devmode.sh passes verification. If the Dev Mode app is installed, uninstall it!
[ ] Dev Mode app installed; uninstall it before rebooting!
[ ] Rooting complete
[ ] Payload complete
```

**Critical notes:**

- After success, **uninstall the Dev Mode app before rebooting**, as the script warns.
