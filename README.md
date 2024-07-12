# Arctic Slime
A SlimeVR Tracker Design by nethesem. This page is a work in progress.

Arctic Slime is inspired by Frozen Slime, designed to be a PCB-based tracker that does not require a case, but addresses the main drawbacks of Frozen. Arctic aims to take advantage of the Li-Ion cell as a way of ditching integrated charging, reducing the number of components and making the charging process as simple as slapping the cells into external chargers. The 14500 (size of a AA) cell is significantly smaller than an 18650, making the overall design extremely simple and compact.

 - Compact design around C3 SuperMini
 - Compatible with common BMI and 'official' BNO IMUs
 - Diode protection and Batt Level Sense
 - 50mm strap loops to fit common cargo straps

![Photo of Arctic Slimes with typical battery charger](photo1.jpg)

Special thanks to;
[frosty6742](https://github.com/frosty6742/frozen-slimes-v2/commits?author=frosty6742) - Frozen Slime concept, I think the PCB with integrated strap loops is a really cool idea.
[gorbit99](https://github.com/gorbit99/tiny-slime/commits?author=gorbit99) - I basically copied TinySlime's SuperMini pinout and batt sense setup, and have heavily plagiarized the TinySlime ReadMe.

## Considerations

The 14500 3.7v Li-ion cell is an oddball size that is difficult to find and not massively space efficient. I use 800mAh cells, I think 1000mAh is possible, but anything more than that is likely a fake in this form factor. As such, these trackers are generally good for about 8hrs run time. This isn't great, but they're also a lot less hassle to charge than most slimes, which is one of the main objectives of this design.

The C3 SuperMini has a terrible antenna, meaning you will need your wireless access point / router to be in the same room.

A case-less tracker like this looks very cool and doens't need 3D printed parts, but is also very exposed. I plan to design an optional 'clip-on cover' at some point, but for now, don't sit on one of these during use.

I have not assigned any particular lisence to this, feel free to use, remix, and resell trackers based on Arctic - I only ask for accreditation. 

## BOM

| Part                                  | Count | Source                                                                       |
| ------------------------------------- | ----: | ---------------------------------------------------------------------------- |
| Arctic Slime PCB                      |     1 | JLCPCB                                                                       |
| Supermini ESP32C3                     |     1 | [AliExpress](https://aliexpress.com/item/1005005877531694.html)              |
| IMU                                   |     1 | [BMI270](https://store.kouno.xyz) or [BNO085](https://shop.slimevr.dev/products/slimevr-imu-module-bno085) |
| AA Battery Holder                     |     1 | [AliExpress](https://www.aliexpress.com/item/1005006254465094.html)          |
| 14500 Battery                         |     1 | [Overlander](https://overlander.co.uk/800mah-3-7v-14500-li-ion-battery.html) |
| 1N5817 diode                          |     1 | [AliExpress](https://aliexpress.com/item/1005002813143363.html)              |
| 1/4w 100kΩ resistor                   |     2 | [AliExpress](https://aliexpress.com/item/1005006358156511.html)              |
| MSS22D18 Switch                       |     1 | [AliExpress](https://aliexpress.com/item/4000699811538.html)                 |

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
