# HiChord Test Firmware Updater

**🔬 Development Environment for Testing Experimental Firmware**

This is a test version of the HiChord firmware updater designed for developers to flash experimental firmware builds during development.

## 🌐 Live URL

**https://hichord.github.io/Test-Updater/**

## ⚠️ Important

- **This is NOT for production use** - For production firmware updates, use the [official updater](https://hichord.github.io/hichord-updater/)
- This updater requires **manual firmware file upload**
- No version tracking or auto-loading of firmware
- Purple theme distinguishes it from production (orange theme)

## 🎯 Purpose

Use this updater to:
- Test experimental firmware builds during development
- Flash custom builds from `.pio/build/unified/hichord_unified.bin`
- Iterate quickly without deploying to production updater
- Validate firmware changes before release

## 🚀 Usage

1. Build your firmware: `pio run`
2. Go to https://hichord.github.io/Test-Updater/
3. Upload your `.pio/build/unified/hichord_unified.bin` file
4. Put HiChord in DFU mode (hold F1+F2+F3 for 5 seconds)
5. Connect via WebUSB
6. Flash firmware

## 📦 What's Different from Production?

| Feature | Production Updater | Test Updater |
|---------|-------------------|--------------|
| **Theme** | Orange accent | Purple accent |
| **Firmware Loading** | Auto-loads from `/firmware/` | Manual file upload only |
| **Version Display** | Shows firmware version/MD5 | No version tracking |
| **Target Audience** | End users | Developers |
| **URL** | hichord.github.io/hichord-updater | hichord.github.io/Test-Updater |

## 🔧 Technical Details

- Uses same DFU protocol implementation as production
- Supports drag-and-drop file upload
- Flashes to QSPI at `0x90040000` (same as production)
- Respects QSPI linker gap for `.qspidata` section
- WebUSB-based (Chrome/Edge only)

## 📝 QSPI Memory Layout

From `src/hichord_seed.ld`:
```
QSPIFLASH: 0x90040000 (512KB reserved for firmware)
QSPIDATA:  0x900C0000 (samples/data region)
Gap:       0x80000 (512KB)
```

The unified binary includes both SRAM and QSPI sections, with the deploy script extracting the actual QSPI offset dynamically.

## 🔗 Related Repositories

- [HiChord Firmware](https://github.com/HiChord/HiChord) - Main firmware source
- [Production Updater](https://github.com/HiChord/hichord-updater) - Official firmware updater
- [Manual](https://github.com/HiChord/hichord-manual) - User manual

## 📄 License

Same as HiChord firmware (check main repository)
