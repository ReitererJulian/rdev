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

`Node Path` to set if json files will be saved. Parameter `bool` 

```
Storage.Control.SaveMeasurementData
```

Simple example:
```python
url: str = "opc.tcp://ESF00000000fc2f4839:4840"
client = Client(url)
client.connect()
node = client.get_node(f"ns=2;s={"Acceleration.Data.RawData.DataLink"}")  
return node.get_value()
client.disconnect()
```


# Sensor Setup & Testing Guide

## 1. Connect to the Sensor

- Connect to the sensor using its **IP address** or **hostname**.
    
- For Wi-Fi, the network is usually called **EDS-INIT**.
    
- Depending on the sensor version, the Wi-Fi name may also be available:
    
    - **IFE_Sensors**
        
    - **IFE_SENSORS**
        

---

## 2. Verify Data in Grafana

The final setup step is to ensure that the sensor data appears in **Grafana**.

### Testing Dashboard

In the **Testing Dashboard**, you can:

- Compare multiple sensors.
    
- Start a **manual measurement**.
    
- Shake the sensor slightly.
    
- If new data appears in Grafana after shaking the sensor, the setup is working correctly.
    

---

## 3. Bluetooth Measurements

- Open **Essence Vibro**.
    
- Select the **Bluetooth** symbol.
    
- If the connection does not work the first time, try connecting a second time.
    

---

## 4. Modbus Test Setup

Verify Modbus communication by checking that:

- A command is sent over the cable.
    
- The sensor returns the expected response.
    

---

## 5. Configuration

The current sensor settings can be viewed under:

**Config**

---

## 6. Software Updates via SSH

### New Sensors

```bash
ssh eds@<IP_ADDRESS>
```

- password: `inital`
    

### Older Sensors

```bash
ssh pi@<IP_ADDRESS>
```

Become the root user:

```bash
sudo su
```

From there, you can install or uninstall updates as required.

### Update Commands

#### Dev Version

Install the dev version (1.0.13)
This version has the updated clock

```bash
pip install InvenSense9DOFBuffered==1.0.13.dev0+feat.pllclock127 --index-url "https://poly:REDACTED.01.0y153gksk@git.esenseial.at/api/v4/projects/153/packages/pypi/simple" --break-system-packages
```

#### Stable

Command to install the older stable version without the updated clock

```bash
pip install InvenSense9DOFBuffered==1.0.12 --index-url "https://poly:REDACTED.01.0y153gksk@git.esenseial.at/api/v4/projects/153/packages/pypi/simple" --break-system-packages
```

### Raw Data file Location

After triggering a measurement with the essence app the file is saved into this directory as JSON's:

`Documents\measurement\raw_acceleration`


### Sensor Error

If **Continuous Measurement** was enabled on an older firmware version, the sensor may end up with an extremely long queue of measurements after a restart. This happens because the sensor's internal clock only synchronizes after boot, until then, it still thinks the old time is correct.

For example: if the sensor was turned off at `12:00` and turned back on at `14:00`, it will initially believe it's still `12:00`. After a few minutes, once the clock syncs, it realizes 2 hours have passed and tries to queue and run all measurements that were missed during that time.

Until this queue is empty it puts new measurement requests at the end, so the sensor becomes unresponsive.

**Fixed** in version `1.0.13`, or can be worked around by restarting the Omega2.


### Testing

-          SMS00000000a4cea30c 

-          SMS000000005843f8af

-          SMS000000005bea90ac

First:

All with 1.0.12


