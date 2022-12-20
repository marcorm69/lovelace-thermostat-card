# lovelace-thermostat-card
A new thermostat card for Home Assistant

## Description

This is not the classic Home Assistant card, but only a yaml configuration which gives the opportunity to manually create a more appealing thermostat card than the default one.  
In the future, depending on the my free time, I can may try to turn it into an installation with HACS.  
There are currently no repositories to add, js to install or anything. All code is based on yaml.  

![image](https://user-images.githubusercontent.com/18568434/208685340-16774dad-45d2-4f5c-830e-46a6dfb75725.png)

## Prerequisite

In addition to the default HA cards you will need to install the following cards:
  
* [custom:mod-card](https://github.com/thomasloven/lovelace-card-mod)
* [custom:layout-card](https://github.com/thomasloven/lovelace-layout-card)
* [custom:button-card](https://github.com/custom-cards/button-card)
  
All cards can be installed via [HACS](https://github.com/hacs/integration)

## Introduction

This version consists of the following files:

* **/config/config_climate.yaml**  
  Contains sensors, binary sensors, history_stats and utility meeter to create create before the card installation and configuration   
  
* /templates/template_button_climate.yaml  
  Contains the template for custom button card.  
  **This file can be used for all the valves\thermostats without needing to be duplicated and configured for each of them**
  
* /lovelace/climate_card_studio.yaml  
  Contain the master structure for card

* /lovelace/climate_studio.yaml  
  Contain the card structure for thermoatat  

* /lovelace/thermostat_card_studio.yaml  
  Contain the thermostat card definition.  
  **This file can be used for all the valves\thermostats without needing to be duplicated and configured for each of them**
 

## Installation and configuration  

This code is written for Netatmo Valve, it is possible that other valves and/or thermostats have different names, attributes, states and sensors.
Refer to your devices for configuration.

### Sensors and other

In **/config/config_climate.yaml** you can find the base set to install for full card operation.  
You can insert in the existent config files (configuration.yaml, sensor.yaml or other) or use as package. Depending your configuration.  
If you have multiple valves/thermostats, just duplicate the various sensors by changing only the entity.  
  
***Possible configuration***  
  
- In the **- platform: statistics** you can change hours to monitor to calculate the min and max temperature.  
  By default is 168h (one week)

### Templates

In **/templates/template_button_climate.yaml** you can found the style for the custom button card used. You can change color, border and various style.

### Cards

