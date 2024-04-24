# nodered-sonnen-nrgkick-flow
This nodered flow reads PV data from the status endpoint of a Sonnenbattery and provides it in specific custom api format to a nrgkick for PV-led charging.

Documentation of PV-led charging with nrgkick is provided by the manufacturer:  
https://www.nrgkick.com/en/pv-charging/  
There you can also find a description of the custom api solution.

# Usage
To adapt the flow you have to change values in following nodes
* *deviceInfo*: provides info about your PV setup to nrgkick regarding inverter capacity max battery storage
* *Sonnenbatterie Status*: url of your Sonnenbatterie status endpoint

## Without Sonnenbattery
If you have a different or no battery you have to change the nodes "Sonnenbatterie Status", "transform sonnen values" and "values"
so it reads PV data from a different endpoint, transforms it (if needed) and provides it in appropriate fields of the response json.
