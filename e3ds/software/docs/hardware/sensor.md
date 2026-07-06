# Sensors

Documentation for the `Esenseial Sensors`  

## Sensor Types

Both sensors have nearly the same hardware built into them. The S-Type has no battery and the M-Type has a battery. 
But both sensors use a `Raspberry PI Zero 2WH` with the sensor sandwiched on top and connected using the gpio pins

### ESF-S

The `ESF-S` is the `Stationary` version with a 24V power in and no battery

Full model name:

`ESF-S: SES00000000567f49fa` -> Stationary 

---

### ESF-M

The `ESF-M` is the `Modular` version with a battery 

Full model name:

`ESF-M: ESF00000000fc2f4839` -> Modular

---


## Access

The sensors can be accessed via different ways.

For the first start it is recommended to use the `RS458` Interface to set the device up.
After the initial setup Wi-Fi is the standard to access it  

### RS485

To connect to the sensor before setting it up for Wi-Fi use, the `RS485 8-Pin` cable is used.
Connect the sensor via a USB-Adapter to you PC and use the `Device-Manager` to find the right serial port (`COM` Port).

Example:
`COM6`

#### Putty

After plugging in the `RS485` Cable using a USB Adapter open putty and switch to serial mode.

Select the `COM`  Port which the sensor is using and enter these connection Parameters:

- Speed: `115200`

Other settings can be left standard ore change them to this:

- Data bits `8`
- Stop bits `1`
- Parity `None`
- Flow control `XON/XOFF`

---

### Wi-Fi

There are two methods to access the sensor without using any cables.
This can be done by using `REST` or `OPC UA`

#### REST

To connect to the sensor via `REST` just open a browser and type:  `http://Host:Port`
Using `/` to navigate to other `nodes`

Example:
```
http://esf00000000fc2f4839:8700/status
```

There is a URL to save the raw data `.json` file. This URL changes with every new file.

```
http://10.30.117.246:8700/cache/50c6e2d8-7259-4da2-adce-74fc7edfc14b-raw.json
```

#### OPC UA

To connect via `OPC UA`, use an OPC UA Client (like UA Expert) and enter the following Endpoint URL:
`opc.tcp://Host`

Example:
`opc.tcp://esf00000000fc2f4839`

In UA Expert click the `+` Icon to add a Server.
Under the point `Custom Discovery` double click on `<Double click to Add Server...>`
Enter the Host after `opc.tcp://`
Expand this tab twice.

#### OPC UA using Python

The `Rest API` is as far as I know read only. Settings like `Storage.Control.SaveMeasurementData` cant be changed via REST.

`ns=2;i=1` 

`ns=2` -> means namespace 2
- Namespace 0 is reserved for OPC UA standard nodes
- Namespace 1 is reserved for the server itself
- Namespace 2 is for custom nodes

NodeID to set if json files will be saved: 

```
Storage.Control.SaveMeasurementData
```