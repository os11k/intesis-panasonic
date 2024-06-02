# intesis-panasonic
Simple control of Panasonic heat pump via Modbus TCP (WiFi) directly to HA using Intesis PAW-AW-MBS-H/PA-AW2-MBS-1(INMBSPAN001A000).

With this, you can currently:
- Change operation modes: off, heat, heat with tank, and tank.
- Set the desired temperature for heat and tank.
- View alarms, temperatures, energy consumption, etc.

Limitations:
- The manual mentions several additional modes: auto, cool, and cool with tank. I personally don't plan to use them and didn't include them in this config, but this functionality can be easily extended if you look in my code.
- I control heat using a compensation curve, which means the min/max temperature setpoint is -5/5 ºC, and this is hardcoded. So, check what the min/max setpoints are and update panasonic_tank_climate accordingly.
- Only one zone is supported; adding a second zone should be quite straightforward.


Sources:
* Modbus codes: https://hmsnetworks.blob.core.windows.net/nlw/docs/default-source/products/intesis/manuals-and-guides---manuals/user-manual-inmbspan001a000.pdf?sfvrsn=193150d7_15

Compatibility list:

* https://hmsnetworks.blob.core.windows.net/nlw/docs/default-source/products/intesis/manuals-and-guides---reference-guides/intesis_inxxxpan001a000_compatibility-list.pdf?sfvrsn=546951d7_11

My Control Panel is very simple, and the code is in this repository under the `user_interface` folder.

<img src="https://i.imgur.com/nmqSxJz.png" width=40% height=40%>

Hardware required (for my setup):
- Intesis PAW-AW-MBS-H/PA-AW2-MBS-1(INMBSPAN001A000)
- A Modbus TCP converter. I use the Waveshare RS485 PoE(https://www.waveshare.com/wiki/RS485_TO_ETH_(B))

How to install this:
- Copy the packages folder to your HA installation folder and modify `configuration.yaml` to include this part:
```
homeassistant:
  packages: !include_dir_named packages
```
- Modify panasonic.yaml with your working Modbus settings.
- Verify that HA configuration is OK and reboot.
- Copy my HA UI card layouts if you'd like.

How to configure RS485 PoE:

I found this video very useful for configuring RS485 PoE; it was not so straightforward, at least for me:

* https://www.youtube.com/watch?v=wEasws0fIVg&t=1794s

Wiring (all DIP-switches have default configuration):

<img src="https://i.imgur.com/vsKi3i6.jpg" width=40% height=40%>

My settings that work for my RS485 PoE:

<img src="https://i.imgur.com/jFMEWii.png" width=40% height=40%>

<img src="https://i.imgur.com/ZH2ZEIj.png" width=40% height=40%>
