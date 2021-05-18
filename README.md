# My Home Assistant Configuration
I'm maintaining this more as a way of reminding myself what hardware I'm using, and where I bought it.
(And also for reminding me what I'm planning to use other hardware for)

This all started off when we bought our new home and had a Hive system installed for controlling our heating.
I bought bought a light bulb, and power socket that could also be controlled with it, then I just kept adding to it.

The problem with Hive was/is that latency sucks - even with the plug and bulbs being locally controlled via the Hive Hub over a radio based protocol called
zigbee - communicating with the Hub via the Hive app on my phone required internet based comms to an AWS hosted server. Gotta hate it when servers go down...

Home Assistant is a much more local solution that doesn't require IoT comms, unless you want it to - and so I got hooked :-)

## Hardware ##
I'm running Home Assistant on a 4GB Raspberry PI 4 model B, with a 32 GB SD card, using a Conbee II usb stick for integrating/controlling Zigbee lights, plugs, and sensors.


### 🐝 Zigbee ###

| Model                                                        | Image                                                                  | Quantity | Notes                                                        |
| ------------------------------------------------------------ | ---------------------------------------------------------------------- | -------- | ------------------------------------------------------------ |
| Aqara human body movement and illuminance sensor [RTCGQ11LM] | ![Aqara Motion](https://www.zigbee2mqtt.io/images/devices/RTCGQ11LM.jpg)           | 6        | Used to detect motion, and occupancy - lights turn on/off accordingly. |
| Aqara door & window contact sensor [MCCGQ11LM]               | ![Aqara Door/Window](https://www.zigbee2mqtt.io/images/devices/MCCGQ11LM.jpg)      | 6        | Turn lights on/off when doors are opened, closed etc. |
| Aqara light sensors              [GZCGQ11LM]                 | <img src="https://zigbee.blakadder.com/assets/images/devices/Aqara_GZCGQ11LM.jpg"> | 4        | The PIR sensors only take illuminance readings when motion or occupancy is detected. These give continuous readings, so non-PIR based automations can factor in these readings |
| Heiman Power Monitoring Plug     [HS2SK]                     | <img src="https://zigbee.blakadder.com/assets/images/devices/Heiman_HS2SK.jpg">    | 2        | Monitor washing machine and tumbledryer, notify me when finished |
| Hive Plug                        [1613V]                     | <img src="https://zigbee.blakadder.com/assets/images/devices/Hive_1613V.jpg">      | 1        | Monitor dishwasher, notify me when finished. Way more expensive than Heiman|
| Lidl/SilverCrest Plug             [HG06337-SB]               | <img src="https://zigbee.blakadder.com/assets/images/devices/Lidl_HG06337-BS.jpg"> | 6        | Bedside lamps, heaters, kettle |
| Lidl/SilverCrest power strip   3 plugs [HG06338]             | <img src="https://zigbee.blakadder.com/assets/images/devices/Lidl_HG06338.jpg">    | 1        | Used in my study for external monitors, laptop charger, and USB hub. |


### Lighting ###

| Model                             | Image                                                                                        | Quantity | Notes                                                            |
| ----------------------------------|--------------------------------------------------------------------------------------------- | -------- | ---------------------------------------------------------------- |
| eWeLight                          |                                                                                              | 2        | Study and guest room lights.                                     |
| Hive        [HALIGHTDIMWWB22]     | <img src="https://zigbee.blakadder.com/assets/images/devices/Hive_HALIGHTDIMWWB22.jpg">      | 7        | Lights in hall, kitchen, landing, laundry room  and cloakroom.   |


