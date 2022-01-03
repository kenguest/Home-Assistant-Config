# My Home Assistant Configuration
I'm maintaining this more as a way of reminding myself what hardware I'm using, and where I bought it.
(And also for reminding me what I'm planning to use other hardware for)

This all started off when we bought our new home and had a Hive system installed for controlling our heating.
I bought a light bulb, and power socket that could also be controlled with it, then I just kept adding to it.

The problem with Hive was/is that latency sucks - even with the plug and bulbs being locally controlled via the Hive Hub over a radio based protocol called
zigbee - communicating with the Hub via the Hive app on my phone required internet based comms to an AWS hosted server. Gotta hate it when servers go down...

Home Assistant is a much more local solution that doesn't require IoT comms, unless you want it to - and so I got hooked :-)

## Hardware ##
I'm running Home Assistant on a 4GB Raspberry PI 4 model B, with a 32 GB SD card, using a [Conbee II usb stick](https://phoscon.de/en/conbee2) for integrating/controlling Zigbee lights, plugs, and sensors.

Some of the plugs have power monitoring, and I've automations set up to send me messages when the dishwasher, washing machine and tumble dryer have finished. These are mostly gleaned from
Phil Hawthorne's excellent [Making ‘dumb’ Dishwashers and Washing Machines Smart: Alerts When the Dishes and Clothes Are Cleaned](https://philhawthorne.com/making-dumb-dishwashers-and-washing-machines-smart-alerts-when-the-dishes-and-clothes-are-cleaned/) article. He also wrote a great article on [managing your shopping list with Grocy and Home Assistant](https://philhawthorne.com/automating-your-shopping-list-with-home-assistant-and-grocy/).

### Wifi ###
| Model | Buy | Image | Notes |
|------|----| ------ |-------- |
| Video Doorbell 2K HD with Intercom | [AliExpress](https://www.aliexpress.com/item/4001286888185.html) | <img src="https://ae01.alicdn.com/kf/H5bc2d5a0f50b48e89d3b0d5d72604a97e/WiFi-Video-Doorbell-2K-HD-Video-Wireless-Camera-Angle-Mount-Motion-Detection-Smart-Door-Intercom-Support.jpg_Q90.jpg_.webp"> | Doorbell, powered via existing doorbell wiring (12/24v), no subscription required. Configure Onvif access through it's own app, and then access on port 8000 through Home Assistant|


### 🐝 Zigbee ###

#### Sensors ####
| Model                                                        | Zigbee Device Compatibility Reference  | Buy  | Image                                                                              | Quantity | Notes                                                        | Battery Type |
|--------------------------------------------------------------|------|------|------------------------------------------------------------------------------------|----------|--------------------------------------------------------------|--------|
| Aqara human body movement and illuminance sensor  |  [RTCGQ11LM](https://zigbee.blakadder.com/Aqara_RTCGQ11LM.html)    | [AliExpress](https://www.aliexpress.com/item/Aqara-Human-Body-Sensor-Smart-Body-Movement-PIR-Motion-Sensor-ZigBee-Wireless-Connection-Aqara-Sensor-For/4001230659983.html)     | ![Aqara Motion](https://www.zigbee2mqtt.io/images/devices/RTCGQ11LM.jpg)           | 6        | Used to detect motion, and occupancy - lights turn on/off accordingly.  | CR2450 |
| Aqara door & window contact sensor                | [MCCGQ11LM](https://zigbee.blakadder.com/Aqara_MCCGQ11LM.html)     | [AliExpress](https://www.aliexpress.com/item/1005001694843048.html)      | ![Aqara Door/Window](https://www.zigbee2mqtt.io/images/devices/MCCGQ11LM.jpg)      | 6        | Turn lights on/off when doors are opened, closed etc. | CR1632 |
| Aqara light sensors                               | [GZCGQ11LM](https://zigbee.blakadder.com/Aqara_GZCGQ11LM.html)     | [AliExpress](https://www.aliexpress.com/item/1-10pcs-Xiaomi-Mijia-Smart-Light-Sensor-Zigbee-3-0-Light-Detection-Intelligent-Linkage-Waterproof-Used/1005001627142486.html)     | <img src="https://zigbee.blakadder.com/assets/images/devices/Aqara_GZCGQ11LM.jpg"> | 4        | The PIR sensors only take illuminance readings when motion or occupancy is detected. These give continuous readings, so non-PIR based automations can factor in these readings. | CR2450 |

#### Switches ####
| Model                                                        | Zigbee Device Compatibility Reference  | Buy  | Image                                                                              | Quantity | Notes                                                        | Battery Type |
|--------------------------------------------------------------|------|------|------------------------------------------------------------------------------------|----------|--------------------------------------------------------------|----|
| Sonoff Wireless Switch    | [SNZB-01](https://zigbee.blakadder.com/Sonoff_SNZB-01.html) | [AliExpress](https://www.aliexpress.com/item/1005001726907261.html) | <img src="https://zigbee.blakadder.com/assets/images/devices/Sonoff_SNZB-01.jpg">| 1 | Switch for bedside lamp. There are three separate types of events: single click, double click, and long click - I have these mapped to on, toggle and off respectively.  [EventSensor](https://github.com/azogue/eventsensor) integration in HACS can be used to make this work under ZHA -  [additional notes on using EventSensor here](https://community.home-assistant.io/t/unable-to-pair-sonoff-zigbee-snzb-01-wb-01-buttons/218324/19), along with some on how to integrate natively. | CR2450 |
| IKEA Tradfri Remote Control | [E1810](https://zigbee.blakadder.com/Ikea_E1810.html)| [Ikea](https://www.ikea.com/ie/en/p/tradfri-remote-control-30443124/)| <img src="https://zigbee.blakadder.com/assets/images/devices/Ikea_E1810.jpg">| 2 | Living Room and Guest room lights, configured using [this Blueprint](https://my.home-assistant.io/redirect/blueprint_import/?blueprint_url=https%3A%2F%2Fcommunity.home-assistant.io%2Ft%2Fzha-ikea-five-button-remote-for-lights%2F253804)| CR2032 |


#### Power plugs/monitoring ####
| Model                                                        | Zigbee Device Compatibility Reference      | Buy      | Image                                                                              | Quantity | Notes                                                        |
| ------------------------------------------------------------ |----- |----- | ---------------------------------------------------------------------------------- | -------- | ------------------------------------------------------------ |
| Heiman Power Monitoring Plug                             | [HS2SK](https://zigbee.blakadder.com/Heiman_HS2SK.html)     | [AliExpress](https://www.aliexpress.com/item/Heiman-Zigbee-Power-Metering-Plug-EU-UK-US-Wall-socket-Control-Power-On-off-For-Smart/32839165490.html)     | <img src="https://zigbee.blakadder.com/assets/images/devices/Heiman_HS2SK.jpg">    | 2        | Monitor washing machine and tumbledryer, notify me when finished |
| Hive Plug                                                  | [1613V](https://zigbee.blakadder.com/Hive_1613V.html)     | [Amazon.co.uk](https://www.amazon.co.uk/Hive-ICESMRTPLUG-Active-Smart-Plug/dp/B01N7L53TB/)     | <img src="https://zigbee.blakadder.com/assets/images/devices/Hive_1613V.jpg">      | 1        | Monitor dishwasher, notify me when finished. Way more expensive than Heiman. Oddly Hive's app doesn't make use of the power monitoring feature on the plug, and they don't market the plug as having this feature. |
| Lidl/SilverCrest Plug                            | [HG06337-SB](https://zigbee.blakadder.com/Lidl_HG06337-BS.html)     |      | <img src="https://zigbee.blakadder.com/assets/images/devices/Lidl_HG06337-BS.jpg"> | 6        | Bedside lamps, heaters, kettle |
| Lidl/SilverCrest power strip   3 plugs                 | [HG06338](https://zigbee.blakadder.com/Lidl_HG06338.html)     |      | <img src="https://zigbee.blakadder.com/assets/images/devices/Lidl_HG06338.jpg">    | 1        | Used in my study for external monitors, laptop charger, and USB hub. |


#### Lighting ####

| Model                   | Zigbee Device Compatibility Reference      | Buy     | Image                                                                                        | Quantity | Notes                                                            |
| ------------------------|------|------|--------------------------------------------------------------------------------------------- | -------- | -------------------------------------------------------------- |
|  RGBW B22 Bulb          | [ZAH-BL01-RGBCW](https://zigbee.blakadder.com/eWeLight_ZAH-BL01-RGBCW.html)    | [eWeLight, RGBW B22 Bulb](https://www.aliexpress.com/item/1005002483909414.html)      |        <img src="https://zigbee.blakadder.com/assets/images/devices/eWeLight_ZAH-BL01-RGBCW.jpg">  | 3        | Study, landing, and cat room lights.                                     |
| ERIA Smart Dimmable Warm White B22 Light Bulb |  | [Eria Smart Dimmable Warm White B22 Light Bulb](https://connectit.ie/products/smart-dimmable-warm-white-b22-light-bulb-eria-a60-9w) |  | 1 | Main light for guest room. |
| Hive Dimmable B22 Bulb  | [HALIGHTDIMWWB22](https://zigbee.blakadder.com/Hive_HALIGHTDIMWWB22.html)     | [Amazon.co.uk](https://www.amazon.co.uk/Hive-Lights-Dimmable-Bayonet-Smart/dp/B01I3T67EC/)     | <img src="https://zigbee.blakadder.com/assets/images/devices/Hive_HALIGHTDIMWWB22.jpg">      | 7        | Lights in hall, kitchen, landing, laundry room  and cloakroom.   |


## Software ##

### Integrations ###
These are some of the integrations that I have set up for either day-to-day or occasional use.

#### [AVM Fritz!Box Tools](https://www.home-assistant.io/integrations/fritz/) ####
Used for presence detection, and for remotely rebooting/reconnecting the Internet connection.

#### [EventSensor](https://github.com/azogue/eventsensor) ####
Installed via HACS and used to make the Sonoff wireless switch events show as distinct/eaiser debugged in the Logbook -
[additional notes on using EventSensor here](https://community.home-assistant.io/t/unable-to-pair-sonoff-zigbee-snzb-01-wb-01-buttons/218324/19), along with some on how to integrate natively. 


#### [Hive](https://www.home-assistant.io/integrations/hive/) ####
Used for controlling the Hive thermostats.

#### [HP Printer](https://github.com/elad-bar/ha-hpprinter) ####
Ink levels, and also number of pages printed and scanned.

#### [Garbage Collection](https://github.com/bruxy70/Garbage-Collection) ####
Sensor for notifications of scheduled collections, extremely configurable and
very hard to notice which is just what I need.

Just set up one entity for each separate type of collection (e.g. one for
compost day, and another for recycling if they're not collected on the same
day) and set the recurrence rules and icon/display accordingly.

#### [Met Eireann](https://www.home-assistant.io/integrations/met_eireann/) ####
Uses the Irish Meteorological Service weather forecast API to display weather
information in Home Assistant.

#### [Workday](https://www.home-assistant.io/integrations/workday/) ####
I'm using the Workday binary sensor integration so that work related
automations only get triggered on days that I'm supposed to be working on -
e.g. standard work week with Bank Holidays taken into consideration.
This means that monitors don't get turned on automatically on weekends or any
other day when I shouldn't need them.
