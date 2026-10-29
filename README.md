# Baofeng Web-Based Programmer

**Program Baofeng radios from the browser.** Bluetooth for the UV-5R Mini and other Bluetooth models, and a USB cable or a TIDRADIO BL-1/BL-2 wireless programmer for the rest. Nothing to install.

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

Pick your radio from the **Radio model** list before connecting. The page starts with no model chosen; opening a CHIRP `.img` file picks the right model for you, including older images without CHIRP's model tag (it checks the firmware or radio ID stored in the image, as CHIRP does).

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
| 5RM, K6, BF-F8HP Pro (also K5-Plus, MaxTalker P15, MaxTalker MT-5RM) | USB cable | Experimental |
| UV-5G Plus, GM-5RH | USB cable | Experimental |
| UV-9R Pro, UV-9R (CHIRP's BF-A58, also RH5X) | USB cable, 9600 baud | Experimental |
| UV-5G Pro | USB cable, 9600 baud | Experimental. Includes AM airband receive (108–136 MHz) |
| F-11 | USB cable, 9600 baud | Experimental |
| Radioddity UV-5RX3 | USB cable, 9600 baud | Experimental. Tri-band |
| Radioddity UV-82X3 | USB cable, 9600 baud | Experimental. Tri-band |
| Radioddity GT-5R | USB cable, 9600 baud | Experimental. Transmits only on 144–148 and 420–450 MHz; channels outside those bands are saved as receive-only |
| UV-9G | USB cable, 9600 baud | Experimental |
| BF-A58S, UV-82III | USB cable, 9600 baud | Experimental. Tri-band |
| UV-S9X3 | USB cable, 9600 baud | Experimental. Tri-band |
| 5RX | USB cable, 9600 baud | Experimental. Tri-band |
| UV-82WP | USB cable, 9600 baud | Experimental |
| GT-3WP | USB cable, 9600 baud | Experimental |
| UV-6R | USB cable, 9600 baud | Experimental |
| DM-32UV / DM-32 (DMR) | USB cable | Experimental. See the note below |

**Experimental** means the model's memory layout, settings and clone protocol come straight from CHIRP's driver and are checked byte for byte against CHIRP, but nobody has tested this programmer on that radio yet. Read first, save a backup `.img`, and please report how it went in a [GitHub issue](https://github.com/drexjj/FengRadioProgrammer/issues).

As a safety check, the programmer refuses to write when the connected radio identifies as a different model from the one selected (for example a UV-5R Mini while UV-32 is selected), or when it isn't the radio you read.

### TIDRADIO BL-1 / BL-2 wireless programmer

Radios without built-in Bluetooth can be programmed wirelessly with a TIDRADIO BL-1 or BL-2 plugged into the mic/speaker jack. Pick your radio, turn it on with the volume up, and click **BL-1/BL-2 adapter** (it shows up as `TIDRADIO KIT` in the pairing window). The adapter sets the serial speed itself; the programmer shows the rate it chose in the status bar.

It's offered for every cable-programmed model on this page except the DM-32UV: the UV-5R family (UV-5R, UV-5R8W, UV-5X, Tenway UV-5R Pro, RT5R, A-5R and others), UV-82 / UV-82 Pro, BF-F8HP, UV-82HP, UV-5G Pro, F-11, UV-5RX3, UV-82X3, GT-5R, UV-9R Pro / UV-9R, UV-9G, BF-A58S / UV-82III, UV-S9X3, 5RX, UV-82WP, GT-3WP, UV-6R, and the UV-17Pro family cable models (UV-17Pro, UV-17Pro GPS, UV-17R Plus, UV-25, UV-32, UV-21Pro, 5RM, UV-5RM Plus / AR-5RM, UV-5RH, K6, BF-F8HP Pro, K5-Plus, MaxTalker P15 / MT-5RM, UV-5G Plus, GM-5RH). TIDRADIO lists the UV-5R, UV-82, UV-5RM, UV-17Pro GPS, UV-25 and UV-9R Pro among the adapter's supported radios. Adapter support is new: please report results in a GitHub issue.

The USB models need a Baofeng programming cable (the two-pin K-plug type). On Windows, install the cable's driver first (usually CH340 or Prolific).

**DM-32UV:** you can edit analog and DMR channels (mode, color code, time slot, TX contact, RX group list, radio ID, scan list, squelch) and the radio's settings. Contacts, RX group lists, radio IDs, zones and scan lists are kept as they are on the radio; edit those in the Baofeng software or CHIRP for now. Deleting a channel also removes it from zones and scan lists, as CHIRP does, and moving channels is turned off because zones and scan lists refer to channel numbers. Writing only sends the 4 KB flash pages that changed and reads each one back to check it. A radio with a programming password is refused. Some CH340 cables corrupt data from this radio; an FTDI or CP2102 cable is recommended.

Not supported yet: BF-5RH Pro (CHIRP has no finished driver for it), UV-19 BT and GMRS-only models such as GM-30.

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

The radio's Bluetooth module is a serial bridge (characteristic `FFE1`), so Bluetooth and the USB cable carry the same clone protocol. The TIDRADIO BL-1/BL-2 is the same idea on the mic/speaker jack: service `FF00`, data out on `FF02` and back on `FF01`, and an `AT` command channel (`FF22`/`FF21`) that reports the adapter's name and the baud rate it settled on. The programmer has four protocol engines:

- **UV-17Pro family** (UV-5R Mini, UV-17Pro, UV-25, UV-32, K6 and others), ported from CHIRP's `baofeng_uv17Pro.py`: a 16-character handshake such as `PROGRAMCOLORPROU`, 64-byte block reads, 64- or 128-byte block writes, and XOR data encryption, at 115200 baud.
- **Classic UV-5R family** (UV-5R, BF-F8HP, UV-82), ported from CHIRP's `uv5r.py`: a 7-byte magic handshake sent byte by byte, `S`/`X` block commands at 9600 baud, and CHIRP's firmware and aux-memory checks before writing.
- **Baofeng common family** (UV-9R Pro / BF-A58), ported from CHIRP's `baofeng_common.py` and `baofeng_wp970i.py`: the same `S`/`X` block commands at 9600 baud with an `AA…DD` ident, a straight 8 KB memory read, and CHIRP's aux-memory checks before writing.
- **DM-32UV** (DMR), ported from CHIRP's `baofeng_dm32uv.py`: `PSEARCH`/`PROGRAM` handshake at 115200 baud, a scan of the radio's tagged 4 KB flash pages, page reads, and verified page writes.

Each model is a profile generated from its CHIRP driver: memory regions, channel layout, power levels, bands, and a byte-level table for every setting found by having CHIRP apply each option and recording what changed. The decoders and encoders are tested against CHIRP's own sample images for every model, and every model completes a read and write against a simulated radio.

## 🌟 Support the Project

If you find this application valuable or have benefited from using it, please consider supporting my work. Every donation, big or small, helps us keep development going.

💖 [Support My Work and Give Thanks](https://buymeacoffee.com/w9jes/membership) or make a one-time donation [here](https://www.paypal.com/donate/?hosted_button_id=SWPB76LVNUHEY) 💖

Can't donate? No worries! Spreading the word and confirming more models also makes a big impact.

Thank you for your support!

## Disclaimer

This is a hobby project, not affiliated with Baofeng or CHIRP. Always save a backup before writing to your radio. You are responsible for transmitting only on frequencies you are licensed for.

## Credits

- Created by **W9JES** with contributions from [others](https://github.com/drexjj/FengRadioProgrammer/graphs/contributors)
- Radio protocols, memory layouts and settings from the [CHIRP project](https://github.com/kk7ds/chirp) and its contributors.


## License and Copyright

Copyright © 2026 JJ (W9JES). All rights reserved, subject to the permissions granted by the license below.

FengRadioProgrammer is made available under the **PolyForm Noncommercial License 1.0.0**.

You are permitted to use, modify, and redistribute this software for noncommercial purposes, subject to the terms and conditions of the license.

Commercial use, including commercial distribution or incorporation into commercial products, is not permitted unless expressly authorized by the license or by separate written permission from the copyright holder.

The original author retains copyright in the original work. This license does not grant permission to use the author's name, project name, or branding to imply endorsement of modified versions.

For the complete terms, permitted uses, exceptions, and conditions, see the `LICENSE` file included with this repository.

For commercial licensing inquiries, please contact the copyright holder through the project's GitHub repository.

