# Sensors

Documentation for the `Esenseial Sensors`  

## Sensor Types

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

#### Putty

Open putty and switch to serial mode.

Select the `COM`  Port and enter these connection Parameters:

* Speed: `115200`

Other settings can be left standard

---

### Wi-Fi

Two methods to access the sensor.
Using `REST` or `OPC UA`

#### REST

To connect via `REST` just open a browser and type:  `http://Host:Port`
Using `/` to navigate to other `nodes`

Example:
```
http://esf00000000fc2f4839:8700/status
```

URL to save the raw data `.json` file:

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