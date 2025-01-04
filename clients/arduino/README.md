# Arduino Client library

Examples are included for ESP32 based devices with either an ST7789V2 IPS LCD (240x280) or an RM67162 AMOLED (240x536) screen.

Development platforms for those have been:
- [LILYGO T-Display-S3 AMOLED](https://lilygo.cc/products/t-display-s3-amoled)
  - ESP32-S3
  - RM67162 AMOLED (240x536)
- [Waveshare ESP32-S3-LCD-1.69](https://www.waveshare.com/wiki/ESP32-S3-LCD-1.69)
  - ESP32-S3
  - ST7789V2 IPS LCD (240x280)

## User API

Configuration parameters should be limited to:
- WifiSsid
- WifiPassword
- ServerHostname
- UniqueId (can instead be derived from the client's mac address)

The library provides the class `FloatingSketchesClient` that holds all data and methods for the user.


