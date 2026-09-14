# Sensor Setup

## Overview

This guide explains how to connect to a sensor, change its configuration, update the software, and compare different software versions.

## Connecting

1. Open the **Essence Updater** application.
2. Enter the sensor's **hostname** or **IP address**.
3. Click **Connect**.
4. Wait until the connection has been established.

If this is not working another possible way of accessing the sensor is using `shh`

Newer sensors:

```bash
ssh eds@<IP_ADDRESS>
```

Older sensors:

```bash
ssh pi@<IP_ADDRESS>
```

## Configuration

After connecting successfully, open the **Config** page in the `Essence Updater` to view the current sensor configuration.

If needed change the settings accordingly:

### SES

For the stationary sensor:

```json 
{  
  "SES": {  
    "Acceleration.Configuration.Frequency": 4500,  
    "Acceleration.Configuration.Sensitivity": 16,  
    "Acceleration.Configuration.Timespan": 2.0,  
    "Acceleration.Control.ContinuousInterval": 10,  
    "Acceleration.Control.ContinuousMeasurement": true,  
    "Communication.Amqp.Enabled": true,  
    "Visualization.Control.PlotResults": true  
  }
}
```

### SMS

For the mobile sensor copy the same as for the stationary but toggle `continuousMeasuerement`:

```json
{
"SMS": {  
    "Acceleration.Configuration.Frequency": 4500,  
    "Acceleration.Configuration.Sensitivity": 16,  
    "Acceleration.Configuration.Timespan": 2.0,  
    "Acceleration.Control.ContinuousInterval": 10,  
    "Acceleration.Control.ContinuousMeasurement": false,
	"Communication.Amqp.Enabled": true,  
	"Visualization.Control.PlotResults": true  
	}
}

```


## Bluetooth Test

Using the **Essence Vibro** app: 

1. Connect to the sensor via Bluetooth. 
2. Start a single measurement. 
3. Shake the sensor slightly. 
4. Verify the output of the measurement

## Software Update

Connect to the sensor via SSH before installing a software update.

### Stable Version

Log in to the sensor:

Install the stable package using the appropriate `pip install` command.
- Version: `10.0.12`

### Developer Version

Log in to the sensor using SSH and install the development package using the provided `pip install` command.
- Version: `10.0.13`

### Compare Changes

After installing a different software version:

- Verify that the installation completed successfully.
- Confirm the installed version in the **Config** page.
- Perform a test measurement.
- Compare the sensor behavior and measurement results with the previous version.
- Check that data is correctly transmitted to Grafana.