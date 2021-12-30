# Linux on Lenovo Yoga/IdeaPad Slim 7 Carbon (AMD)

> Inspired by https://github.com/nekr0z/linux-on-huawei-matebook-13-2019

The laptop was released in Nevember 2021. Full name in Europe "[Lenovo Yoga Slim 7 Carbon Gen 6 (14" AMD)](https://www.lenovo.com/de/de/laptops/yoga/yoga-slim-series/Yoga-Slim-7-Carbon-Gen-6-14-inch-AMD/p/LEN101Y0006)", "Lenovo IdeaPad Slim 7 Carbon Gen 6 (14" AMD)".

Tested specifications:

- Processor: AMD Ryzen™ 7 5800U-Prozessor
- RAM: 16 GB LPDDR4X 4266MHz
- 1 TB M.2 2280 SSD
- Screen: 14.0" 2.8K (2880x1800) OLED, Multitouch
- Graffic card: integrated AMD

Tested disctribution:

- Ubuntu 21.10
- Kernel: 5.13.0.22

## Linux support

| Function | Details | Status | Notes |
| --- | --- |  :---: | --- |
| Processor | Processor: AMD Ryzen™ 7 5800U-Prozessor | ✔ Yes | All 16 cores work out of the box |
| Graphics | Integrated AMD Radeon | ✔ Yes | via standard kernel driver |
| RAM | 16 GB LPDDR4X 4266MHz | ✔ Yes | 13,5G were recognized |
| Display | 14.0" 2.8K (2880x1800) OLED, Multitouch | ✔ Yes | Resolution is correctly detected by `xrandr`, 200% scaling was activated by default and looks good. Automatic brightness adjustment works out of the box. Multitouch works out of the box. |
| Storage | 1 TB M.2 2280 SSD | ✔ Yes | Via standard kernel driver |
| Wifi | Realtek | ✔ Yes | Works out of the box on Ubuntu. Did not work on `POP!_OS` |
| Bluetooth | Bluetooth 5.0| ✔ Yes | Works as expected |
| Speakers  | Dolby | NO | only 2 speakers work |

WIP....
