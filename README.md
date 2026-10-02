# firmware-releases
Firmware OTA Releases 2026

## Factory images (for Apollo, updated 2026-10-01)

Whole-flash images for factory programming: bootloader + partition table + erased otadata + the signed app, and nothing else. No NVS content, no keys, no Wi-Fi credentials. Flash at offset `0x0` on an 8 MB flash, DIO, for example:

```
esptool --chip <esp32c6|esp32s3> --port <port> write_flash 0x0 <image>
```

| Image | Board | App inside | SHA-256 |
|---|---|---|---|
| `apollo-btn1_1_1_3.factory.bin` | BTN-1 (ESP32-C6) | `apollo-btn1_1_1_3.bin` | `7a539db93239724e362357e162ae86cac9faa7adc0b924874f5e8f18c456a568` |
| `apollo-rpro1-mor-retail-count-1.1.8.factory.bin` | R PRO-1 (ESP32-S3) | `apollo-rpro1-mor-retail-count-1.1.8-nvs.bin` | `bc279701097fab87cdf963864922726e62933a94583ee985a109a4d297b420f2` |
| `apollo-rpro1-mor-retail-count-1.1.5.factory.bin` (do not ship) | R PRO-1 (ESP32-S3) | `apollo-rpro1-mor-retail-count-1.1.5-nvs.bin` | `fd5dcbfdabea6cf832e54432522d7321d80be9ded86e03a424085ef4d675d24b` |

**Use `apollo-btn1_1_1_3.factory.bin` for BTN-1 and `apollo-rpro1-mor-retail-count-1.1.8.factory.bin` for R PRO-1.** Both trust release keys 2 and 3. `apollo-btn1_1_1_2.factory.bin` and the R PRO-1 1.1.5 factory image trust only release key 1, which is retired: units flashed with them work but can never be updated over the air. Do not ship either.

A device flashed with one of these boots into the app with no network and no report key; it is then provisioned over USB from the Fleet manager (`/admin/onboard`), which writes the device's key and the store's Wi-Fi. Do not ship `btn_0_6_0.factory.bin` or any credentialed build.
