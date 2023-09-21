# Home Assistant Daikin AC Integration
Clone of the https://github.com/home-assistant/core/tree/dev/homeassistant/components/daikin
## Changes
The official Home Assistant Daikin AC integration is rounding the target temperature to nearest half degree. It's probably doing that to be compatible with some HVAC systems.
```py
def format_target_temperature(target_temperature):
    """Format target temperature to be sent to the Daikin unit, rounding to nearest half degree."""
    return str(round(float(target_temperature) * 2, 0) / 2).rstrip("0").rstrip(".")


class DaikinClimate(ClimateEntity):
    """Representation of a Daikin HVAC."""

    _attr_name = None
    _attr_has_entity_name = True
    _attr_temperature_unit = UnitOfTemperature.CELSIUS
    _attr_hvac_modes = list(HA_STATE_TO_DAIKIN)
    _attr_target_temperature_step = 1
```
Since my AC accepts half degrees, I made the proper changes.

```py
def format_target_temperature(target_temperature):
    """Format target temperature to be sent to the Daikin unit."""
    return str(target_temperature)


class DaikinClimate(ClimateEntity):
    """Representation of a Daikin HVAC."""

    _attr_name = None
    _attr_has_entity_name = True
    _attr_temperature_unit = UnitOfTemperature.CELSIUS
    _attr_hvac_modes = list(HA_STATE_TO_DAIKIN)
    _attr_target_temperature_step = 0.5
```
## Install
1. [Download zip](https://github.com/WZYProjects/HA-Daikin_AC/archive/refs/heads/main.zip)
2. Extract zip
3. Copy the folder **daikin** into **config/custom_components**
4. Restart Home Assistant
