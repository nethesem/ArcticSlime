# Arctic Slime
A SlimeVR Tracker Design by nethesem. This page is a work in progress.

Arctic Slime is designed to be a PCB-based tracker that does not require a case. Arctic aims to take advantage of the Li-Ion cell as a way of ditching integrated charging, reducing the number of components and making the charging process as simple as slapping the cells into external chargers. The 14500 (size of a AA) cell is significantly smaller than an 18650, making the overall design extremely simple and compact.
Special thanks to [frosty6742](https://github.com/frosty6742/frozen-slimes-v2/commits?author=frosty6742), who designed Frozen Slime which was my inspiration for this, and [gorbit99](https://github.com/gorbit99/tiny-slime/commits?author=gorbit99), whose TinySlime design and GitHub I heavily plagurised to utilise the C3 Super Mini.

 - Compact design around C3 SuperMini
 - Compatible with common BMI and 'official' BNO IMUs
 - Diode protection and Batt Level Sense
 - 50mm strap loops to fit common cargo straps

![Photo of Arctic Slimes with typical battery charger](photo1.jpg)

## Pros and Cons

The 14500 3.7v Li-ion cell is an oddball size that is difficult to find and not very space efficient. I use 800mAh cells, I think 1000mAh is possible, but anything more than that is likely a fake in this form factor. As such, these trackers are generally good for about 8hrs run time. This isn't great by slime standards, but they're also a lot less hassle to charge than designs with integrated batteries, and if more run time is needed, two sets can be used with one set on charge and the other in use.

The C3 SuperMini has a terrible antenna, meaning you will need your wireless access point / router to be in the same room.

A case-less tracker like this looks very cool and doens't need 3D printed parts, but is also very exposed. This might not be the design for you if you're expecting a lot of rough-and-tumble usage.

## BOM

| Part                                  | Count | Source                                                                       |
| ------------------------------------- | ----: | ---------------------------------------------------------------------------- |
| Arctic Slime PCB                      |     1 | JLCPCB                                                                       |
| Supermini ESP32C3                     |     1 | [AliExpress](https://aliexpress.com/item/1005005877531694.html)              |
| IMU*                                  |     1 | [BMI270](https://store.kouno.xyz) or [BNO085](https://shop.slimevr.dev/products/slimevr-imu-module-bno085) |
| AA Battery Holder                     |     1 | [AliExpress](https://www.aliexpress.com/item/1005006254465094.html)          |
| 14500 Battery                         |     1 | [Overlander](https://overlander.co.uk/800mah-3-7v-14500-li-ion-battery.html) |
| 1N5817 diode                          |     1 | [AliExpress](https://aliexpress.com/item/1005002813143363.html)              |
| 1/4w 100kΩ resistor                   |     2 | [AliExpress](https://aliexpress.com/item/1005006358156511.html)              |
| MSS22D18 Switch                       |     1 | [AliExpress](https://aliexpress.com/item/4000699811538.html)                 |

*Any IMU that is pin compatible with the two listed options should also work, such as LSM varieties or the BMI160. BNO085 and BMI270 are my current reccomendations.

## Assembly

Assembly video goes here

## Flashing

Trackers can be flashed using the SlimeVR online firmware tool. I reccomend the [Butterscotch version](https://slimevr-firmware.bscotch.ca/).
When flashing, hold the BOOT button on the C3 SuperMini as you connect the USB cable to ensure its in Flash Mode, otherwise flashing will likely fail.

 - Firmware Version:
   - For BNO085 or BMI270, use SlimeVR/main. Other IMUs, consult SlimeVR Discord.
 - Board should be "BOARD_LOLIN_C3_MINI"
   - SDA Pin: 6
   - SCL Pin: 7
   - LED Pin: 8
 - Primary IMU: Select as appropriate
  - If BNO085, INT Pin: 5
 - Secondary IMU: Uncheck (see below)
 - Battery Sense should be BAT_EXTERNAL
   - Battery Shield Resistance: 0
   - Battery Shield R1: 100
   - Battery Shield R2: 100
   - Battery Sense Pin: 1
  
 Aux / Secondary IMU: This PCB does not support Aux IMUs. Given the low-capacity batteries and already compact PCB, it's not a good match up.
