# firmware-releases
Firmware OTA Releases 2026

## Factory images (for Apollo, 2026-09-26)

Whole-flash images for factory programming: bootloader + partition table + erased otadata + the signed app, and nothing else. No NVS content, no keys, no Wi-Fi credentials. Flash at offset `0x0` on an 8 MB flash, DIO, for example:

```
esptool --chip <esp32c6|esp32s3> --port <port> write_flash 0x0 <image>
```

| Image | Board | App inside | SHA-256 |
|---|---|---|---|
| `apollo-btn1_1_1_2.factory.bin` | BTN-1 (ESP32-C6) | `apollo-btn1_1_1_2.bin` | `0ff27bbb1ef02ba38e0336b0055fb5db27603f07208f7a3e24195bbd44aafe82` |
| `apollo-rpro1-mor-retail-count-1.1.5.factory.bin` | R PRO-1 (ESP32-S3) | `apollo-rpro1-mor-retail-count-1.1.5-nvs.bin` | `fd5dcbfdabea6cf832e54432522d7321d80be9ded86e03a424085ef4d675d24b` |

A device flashed with one of these boots into the app with no network and no report key; it is then provisioned over USB from the Fleet manager (`/admin/onboard`), which writes the device's key and the store's Wi-Fi. Do not ship `btn_0_6_0.factory.bin` or any credentialed build.
