This plugin for Loxberry (https://wiki.loxberry.de/) is used to simulate a Fronius SmartMeter with MODBUS TCP protocol.

Note: Text below is automaticaly translated due to lack of time :-) - so please be lenitent.

NOTE: 
This is the TCP version, there's also the RTU version available in another repository. 
Everyone who want's to proceed work with RTU is welcome :-)

Functional Description
======================
The plugin simulates a Fronius Smart Meter in the Modbus TCP network. This means that consumption values can be received via MQTT and forwarded to a Fronius inverter (e.g.: Symo, Symo Hybrid). The data is then permanently stored in the Solarweb statistics.

Installation
============
Installation as usual as ZIP via the Loxberry installation routine.
Installation can take up to 20 minutes depending on the Pi you are using

Prerequisites
=============
An existing SmartMeter that can be read and whose data can be transferred via MQTT.
A Modbus module for the Raspberry
The “MQTT Gateway” plugin must be installed and configured.

Configuration
=============
MQTT Topic current consumption: current consumption (current power) in watts (W)
MQTT Topic Purchase (absolute value): current meter reading for purchased energy in watt hours (Wh)
MQTT Topic Feed-in (absolute value): current meter reading for fed-in energy in watt hours (Wh)
Correction factor: If the data is delivered in kWh via MQTT, it must be converted into Wh =⇒ Correction factor 1000 (default setting).
Port of the Modbus adapter: Port where the Modbus adapter is plugged in.

!!! WARNING !!!
===============
The Fronius inverter does NOT use the "current power in watts" to calculate the current consumption and fill the statistics, but rather calculates this information itself using the difference between the absolute values of the purchase and feed-in in the time window of the query. The data MUST be provided via MODBUS in watt hours (see correction factor description above). If an error occurs when choosing the correction factor, the statistics in the data manager will be falsified.

A falsified statistic can no longer be changed independently!

Of course, this happened to me during my development attempts because I had no idea how the data had to be provided and could only have the statistics corrected by Fronius Support.

Known Issues
============
Configuration data is swapped randomly when saving.

Roadmap
=======
o Solve issue with random saved and swapped data in configuration
o Adding "plausibility check" of data to prevent from destroing Fronius Datamanager values.
o Adding the possibility to simulatre more than 1 smart meter to use it for recording further meters (e.g. heat pump, ...)
