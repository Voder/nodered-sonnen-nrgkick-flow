# nodered-sonnen-nrgkick-flow
This nodered flow reads PV data from the status endpoint of a Sonnenbattery and provides it in specific custom api format to a nrgkick for PV-led charging.

Documentation of PV-led charging with nrgkick is provided by the manufacturer:  
https://www.nrgkick.com/en/pv-charging/  
There you can also find a description of the custom api solution.

# Usage
## Node-RED
To adapt the flow you have to change values in following nodes
* *deviceInfo*: provides info about your PV setup to nrgkick regarding inverter capacity max battery storage
* *Sonnenbatterie Status*: url of your Sonnenbatterie status endpoint

The flow creates 2 endpoints with json responses, as expected by the nrgkick custom api solution:
* /api/v1/info.json
* /api/v1/values.json

Example payloads:  
/api/v1/info.json
```json
{
    "device_info": {
        "inverters": {
            "0": {
                "name": "Sonneninverter",
                "model": "SonneninverterModel",
                "serial": "0123456789",
                "max_dc_w": 20000,
                "max_ac_w": 19500
            }
        },
        "energy_meters": {
            "0": {
                "name": "Sonnenmeter",
                "model": "SonnenmeterModel",
                "serial": "01234567890",
                "location": 1
            }
        },
        "batteries": {
            "0": {
                "name": "Sonnenbatterie",
                "model": "SonnenbatterieModel",
                "serial": "01234567890",
                "capacity_wh": 6000
            }
        }
    }
}
```
/api/v1/values.json
```json
{
  "device_values": {
    "inverters": {
      "0": {
        "inv_power_ac_w": 4869,
        "battery_connected": true
      }
    },
    "energy_meters": {
      "0": {
        "grid_power_w": -4151
      }
    },
    "batteries": {
      "0": {
        "bat_power_w": -5,
        "soc": 100,
        "mode": 0
      }
    },
    "load_power_w": 718
  }
}
```

## Nrgkick
In PV-Charging settings create a new profile. Use "manual search" and "Custom" in the brand selection view.
Insert ip-adress and port of your node-red instance and if the node-red flow works as expected, the nrgkick app should
find your inverter and battery settings.

## Without Sonnenbattery
If you have a different or no battery you have to change the nodes "Sonnenbatterie Status", "transform sonnen values" and "values"
so it reads PV data from a different endpoint, transforms it (if needed) and provides it in appropriate fields of the response json.
