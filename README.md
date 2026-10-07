# Dual Speaker Mod for Redmi Note 9 Pro / 9S [miatoll]

A Magisk / KernelSU module that enables the earpiece as a secondary speaker (pseudo-stereo) for multimedia playback on Snapdragon 720G (`miatoll`).

---

## 📱 Compatibility

* **Target Device:** Redmi Note 9 Pro / 9S / Pro Max / POCO M2 Pro (`miatoll` / SM7125)
* **ROMs:** AOSP-based custom ROMs (crDroid, LineageOS, PixelOS, EvolutionX, etc.)
* **Android Versions:** 14 / 15 / 16
* **Root Solution:** Magisk / KernelSU / APatch

### Test Status
* **crDroid v12 (Android 16):** Fully tested & 100% stable.
* **Other AOSP ROMs:** Compatible (unified vendor audio tree).
* **MIUI / HyperOS:** Untested (backup recommended before testing).

---

## ⚙️ Technical Details

On Snapdragon 720G, the bottom speaker (SmartPA on `TERT_MI2S_RX`) and the earpiece (WCD937x on `RX_CDC_DMA_RX_0`) run on separate hardware buses. 

Direct edits to `mixer_paths` previously triggered a Qualcomm Hexagon DSP crash: q6asm_open_write failed (-61)

This resulted in complete audio failure until reboot.

### Solution implemented:
1. **ACDB Hack:** Set ACDB ID to `10` in `audio_platform_info_intcodec.xml` for simultaneous dual-bus output, bypassing the DSP crash.
2. **Codec Routing:** Routed both interpolators (`RX0 + RX1`) in WCD937x directly to the earpiece DAC (`RDAC3`).
3. **Gain Compensation:** Raised digital gain on the earpiece to balance volume with the bottom speaker.

---

## 🔊 What Works

| Feature | Status | Notes |
| :--- | :---: | :--- |
| **Multimedia Audio** | ✅ | Dual speaker output (YouTube, Spotify, games, etc.) |
| **Earpiece Calls** | ✅ | Stock volume levels (ear-safe) |
| **Speakerphone** | ✅ | Plays via bottom speaker only (no echo / mic feedback) |
| **3.5mm & Bluetooth** | ✅ | Unaffected, stock routing preserved |

---

## 📥 Installation

1. Download the latest `.zip` from **[Releases](https://github.com/EtoKomu/miatoll-stereo-mod/releases)**.
2. Flash via Magisk / KernelSU / APatch.
3. Reboot.

### Uninstallation
Disable or remove the module in your root manager and reboot.

---

## ⚠️ Disclaimer
The earpiece speaker has a physically smaller coil than the bottom speaker. Do not use extreme software bass boosters or excessive digital clipping to prevent hardware wear. Flash at your own risk.
