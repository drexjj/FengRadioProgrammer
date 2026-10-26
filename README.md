# Baofeng Web-Based Programmer

**Program Baofeng radios from the browser.** Bluetooth for the UV-5R Mini and other Bluetooth models, a USB cable for the rest. Nothing to install.

**▶ Open it: [drexjj.github.io/FengRadioProgrammer](https://drexjj.github.io/FengRadioProgrammer/)**

![Baofeng Web-Based Programmer showing the channel grid](docs/screenshot.png)

---

## What it does

Pair the radio, read it, edit everything in a CHIRP-style grid, and write it back. The flow works like the Meshtastic web flasher: you click **Bluetooth**, your browser shows a pairing window, and you pick the radio.

- **Wireless programming** over the radio's built-in Bluetooth. A USB programming cable works too.
- **Every channel**: name, RX/TX frequency, CTCSS/DCS tones, power, FM/NFM/AM, scan, busy-channel lockout, PTT ID, S-code, frequency hopping and RX DTMF.
- **VFO A and B**: frequency, shift, offset, tones, power, bandwidth and step.
- **35+ radio settings**: squelch, beeps and voice, backlight, dual watch, battery save, timeout, VOX, repeater tone burst, tail elimination and more.
- **DTMF**: ANI code and the 20 PTT ID signal codes.
- **Works with CHIRP.** It opens and saves CHIRP `.img` images and CHIRP CSV channel lists, so you can move between the two freely.
- **Backup on every read.** The radio's original image is kept in your browser, and you can save it as a file before you write anything.
- **Quick entry.** In the TX column type an absolute frequency, a shift like `+0.6` or `-5`, or `off` for receive only. Type a frequency into an empty slot to create a channel.
- **Preset channels.** **Add presets** offers ham 2 m/70 cm simplex, GMRS/FRS, MURS, NOAA weather, marine VHF and public-safety interoperability channels. Each has a fixed channel number (ham from 57, the rest from 200 on the 999/1000-channel radios; a compact layout on 128-channel radios), and you tick exactly the ones you want. Receive-only packs are written with TX off.
- **Edit many channels at once.** Tick rows (shift-click for a range) to delete them, change one field across all of them, or export just those channels as a CSV to share.
- **Reorder.** Drag a channel by the ⠿ handle beside its checkbox, or use ▲ ▼.
- **Import lists with a preview.** Opening a CHIRP CSV with **Open file**, such as a repeater list exported from RepeaterBook in CHIRP format or a shared channel pack, shows every row first and fills empty channels from a number you choose instead of overwriting.
- **Undo and redo** for channel, settings and VFO edits (Ctrl/⌘+Z, Ctrl/⌘+Shift+Z).
- **Demo mode.** "Try with a simulated radio" runs the full read and write cycle without any hardware.

## Compatibility

### Radios

Pick your radio from the **Radio model** list before connecting.

| Radio | Connection | Status |
|---|---|---|
| UV-5R Mini, MINI-5 | Bluetooth or USB | ✅ Tested on a real radio |
| UV-5RH | USB cable | ✅ Tested on a real radio |
| UV-5RM Plus, AR-5RM | USB cable | ✅ Tested on a real radio |
| UV-5R (and UV-5R8W, UV-5X, UV-5R EX, UV-5R Pro, UV-5XP, RT5R, A-5R) | USB cable, 9600 baud | ✅ Tested on a real radio |
| UV-82 / UV-82 Pro | USB cable, 9600 baud | ✅ Tested on a real radio |
| BF-F8HP, UV-82HP | USB cable, 9600 baud | ✅ Tested on a real radio |
| UV-5G Mini | Bluetooth or USB | Experimental. GMRS channels 1–30 keep their fixed frequencies |
| UV-28Plus | Bluetooth or USB | Experimental |
| UV-17Pro, UV-17Pro GPS, UV-17R Plus | USB cable | Experimental |
| UV-25 / UV-25 Pro, UV-32 / UV-32 Pro | USB cable | Experimental |
| UV-21Pro V2, UV-21Pro GPS | USB cable | Experimental |
| 5RM, K6, BF-F8HP Pro | USB cable | Experimental |

**Experimental** means the model's memory layout, settings and clone protocol come straight from CHIRP's driver and are checked byte for byte against CHIRP, but nobody has tested this programmer on that radio yet. Read first, save a backup `.img`, and please report how it went in a [GitHub issue](https://github.com/drexjj/FengRadioProgrammer/issues).

As a safety check, the programmer refuses to write when the connected radio identifies as a different model from the one selected (for example a UV-5R Mini while UV-32 is selected), or when it isn't the radio you read.

The USB models need a Baofeng programming cable (the two-pin K-plug type). On Windows, install the cable's driver first (usually CH340 or Prolific).

Not supported: UV-6R, UV-19 BT and GMRS-only models such as GM-5RH and GM-30.

### Browsers

Bluetooth programming uses [Web Bluetooth](https://developer.mozilla.org/docs/Web/API/Web_Bluetooth_API).

| Platform | Browser |
|---|---|
| Windows, macOS, Linux, ChromeOS | Chrome, Edge or Opera |
| Android | Chrome, Edge or Opera for Bluetooth; current Chrome with WebUSB for USB cables |
| iPhone and iPad | [Bluefy](https://apps.apple.com/app/bluefy-web-ble-browser/id1492822055) (Safari has no Web Bluetooth) |
| Firefox, Safari | Not supported |

The USB cable option uses Web Serial on desktop. On Android, the app uses the WebUSB USB-device picker for common CH340, Prolific PL2303 and CP210x cables; use a current Chrome for Android with USB host/OTG support. Bluetooth remains the more widely compatible Android option.

## How to program your radio

1. **Choose your radio model** from the list.
2. **Get the radio ready.** For Bluetooth, open the radio menu, switch Bluetooth on, and return to the main screen. For a USB cable, plug it firmly into the radio and turn the radio on with the volume up.
3. **Connect.** Click **Bluetooth** and pick the radio from the pairing window (it usually shows up as `walkie-talkie`), or click **USB cable** and pick the cable's port.
4. **Read.** Click **Read from radio**. A full read takes about 30 seconds over Bluetooth and 15–30 seconds over USB.
5. **Save a backup.** Click **Save .img** before you change anything.
6. **Edit** channels, VFO, settings and DTMF. Changed rows are highlighted.
7. **Write.** Click **Write to radio** and confirm. Keep the radio close and switched on until it finishes, about 20 seconds.

## Troubleshooting

- **The radio doesn't appear in the pairing window.** Check that Bluetooth is on in the radio menu and that the radio isn't paired to a phone app. If it still doesn't show, open **Log ▸ Bluetooth tuning** and tick **Show every nearby device**.
- **"The radio did not answer the programming handshake."** Make sure the radio is on its main screen, not inside a menu. If you just finished a read or write, turn the radio off and on, then reconnect.
- **Writes stop partway or blocks are rejected.** Keep the write chunk at 20 bytes in **Log ▸ Bluetooth tuning**, or add a 5–10 ms delay between chunks.
- **The browser blocks Bluetooth.** The page must be opened over HTTPS or from `localhost`, in its own tab rather than embedded in another page.
- **Anything else.** Open the **Log** tab, click **Copy log**, and paste it into a [GitHub issue](https://github.com/drexjj/FengRadioProgrammer/issues).

## How it works

The radio's Bluetooth module is a serial bridge (characteristic `FFE1`), so Bluetooth and the USB cable carry the same clone protocol. The programmer has two protocol engines:

- **UV-17Pro family** (UV-5R Mini, UV-17Pro, UV-25, UV-32, K6 and others), ported from CHIRP's `baofeng_uv17Pro.py`: a 16-character handshake such as `PROGRAMCOLORPROU`, 64-byte block reads, 64- or 128-byte block writes, and XOR data encryption, at 115200 baud.
- **Classic UV-5R family** (UV-5R, BF-F8HP, UV-82), ported from CHIRP's `uv5r.py`: a 7-byte magic handshake sent byte by byte, `S`/`X` block commands at 9600 baud, and CHIRP's firmware and aux-memory checks before writing.

Each model is a profile generated from its CHIRP driver: memory regions, channel layout, power levels, bands, and a byte-level table for every setting found by having CHIRP apply each option and recording what changed. The decoders and encoders are tested against CHIRP's own sample images for every model, and every model completes a read and write against a simulated radio.

## 🌟 Support the Project

If you find this application valuable or have benefited from using it, please consider supporting my work. Every donation, big or small, helps us keep development going.

💖 [Support My Work and Give Thanks](https://buymeacoffee.com/w9jes/membership) or make a one-time donation [here](https://www.paypal.com/donate/?hosted_button_id=SWPB76LVNUHEY) 💖

Can't donate? No worries! Spreading the word and confirming more models also makes a big impact.

Thank you for your support!

## Disclaimer

This is a hobby project, not affiliated with Baofeng or CHIRP. Always save a backup before writing to your radio. You are responsible for transmitting only on frequencies you are licensed for.

## Credits

- Created by **W9JES**.
- Radio protocols, memory layouts and settings from the [CHIRP project](https://github.com/kk7ds/chirp) and its contributors.

## License

GPL-3.0. See [LICENSE](LICENSE).

