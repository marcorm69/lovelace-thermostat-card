# lovelace-thermostat-card
A new thermostat card for Home Assistant

## Description

This is not the classic Home Assistant card, but only a yaml configuration which gives the opportunity to manually create a more appealing thermostat card than the default one.  
In the future, depending on the my free time, I can may try to turn it into an installation with HACS.  
There are currently no repositories to add, js to install or anything. All code is based on yaml.  

![image](https://user-images.githubusercontent.com/18568434/208972989-58fc4dd9-8c87-4a48-b141-dc7f7f78f83c.png)
![image](https://user-images.githubusercontent.com/18568434/208973396-f7580bd7-55de-4a63-9e6c-e658151a2b44.png)

## Prerequisite

In addition to the default HA cards you will need to install the following cards:
  
* [custom:mod-card](https://github.com/thomasloven/lovelace-card-mod)
* [custom:layout-card](https://github.com/thomasloven/lovelace-layout-card)
* [custom:button-card](https://github.com/custom-cards/button-card)
  
All cards can be installed via [HACS](https://github.com/hacs/integration)  

> In order to install this card the basic knowledge of HA architecture and yaml is required (sensor, package)  
  
> For advanced configuration (change colors, style, structure or other) the knowledge of css and advanced  knowledge of yaml and HA is reqired 
  
I do not provide support in this regard  
  
  
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

## Installation sensors

In **/config/config_climate.yaml** you can find the base set to install for full card operation.  
You can insert in the existent config files (configuration.yaml, sensor.yaml or other) or use as package. Depending your configuration.  
If you have multiple valves/thermostats, just duplicate the various sensors by changing only the entity.  
  
***Possible configuration***  
  
- In the **- platform: statistics** you can change hours to monitor to calculate the min and max temperature.  
  By default is 168h (one week)

## Installation Templates

In **/templates/template_button_climate.yaml** you can found the style for the custom button card used. You can change color, border and various style.  

## Cards configuration

#### File climate_studio.yaml

Change the entity in:
```yaml
type: custom:button-card
template: climate_thermostat
entity: climate.studio #Change here
```

If necessary, change the attributes and value in:
```yaml
  .therm_on {
      fill:{% if state_attr(config.entity, "hvac_action") == 'heating'  %}  #Change here
             orange   #Change active color
           {% else %}
             #646464  #Change not active color
           {% endif %};
  }
```

If necessary, change the attributes and value in:
```yaml  
  .indicator {
      fill: #fff;
      transform-origin: 50% 50%;      
      transform:  {% set res = {          
            "degree": (state_attr(config.entity, "temperature")*9)-135 #Change here
          }%}
          rotate({{ res.degree }}deg);
  }
```
**ATTENTION** not change degree vaule and operation, is necessary to move the indicator on thermostat

#### File thermostat_card.yaml

This file contains the SVG thermoatat image, it's possible use the same file for all thermostat\valve but you can config, if necessary, the attributes.
At the end of file, you can find the 3 text configurated: set temperature, current temperature, entity name, if necessary, change the attributes
```html  
      <text x="50%" y="30%" class="text_shadow" text-anchor="middle"  font-size="20px" fill="#fff">${entity.attributes.temperature}</text>      
      <text x="50%" y="55%" class="text_shadow" text-anchor="middle"  font-size="62px" fill="#fff">${entity.attributes.current_temperature}</text>      
      <text x="50%" y="68%" class="text_shadow text_area" text-anchor="middle"  fill="#fff">${entity.attributes.friendly_name}</text>   
```
  
On top of the file you can found the card style for text color, fill color,  shadow, font:

```html  
      <style type="text/css">
        .st0{fill:url(#SVGID_1_);}
        .st1{fill:#808080;}
        .st2{fill:#FFFFFF;}
        text {font-family: 'Oswald';}
        .text_shadow {text-shadow: 8px 8px 8px #474747, 19px 19px 3px rgba(255,103,41,0);}
        .text_shadow.text_area {
            font-size: 22px;
            font-family: 'Oswald';
            text-transform: uppercase;
            text-decoration: overline;
         }
      </style>
```

And after the gradient for filling svg image

```html  
      <g>
        <linearGradient id="SVGID_1_" gradientUnits="userSpaceOnUse" x1="25.5" y1="150" x2="274.5" y2="150">
          <stop  offset="0" style="stop-color:#0072BB"/>
          <stop  offset="0.5223" style="stop-color:#FF7B03"/>
          <stop  offset="1" style="stop-color:#8B0000"/>
        </linearGradient>
        <circle class="st0" cx="150" cy="150" r="124.5"/>
      </g>
``` 
