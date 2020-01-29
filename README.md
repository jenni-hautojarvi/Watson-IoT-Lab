# _**Watson IoT platform**_ Lab

## Introduction
In this guide, Step by Step we connect SensiEDGE’s SensiBLE to IBM Watson IoT Platform in IBM Cloud and visualises data in the Node-RED application.

![](./images/Workflow.png)

### Prerequisites
- [IBM Cloud](https://cloud.ibm.com) account
- Sensor, In this lab we use SensiEDGE’s SensiBLE

# Step 1. Connect SensiEDGE’s SensiBLE to ST BLUEMS APP to read data

### SensiEDGE’s SensiBLE

The SensiBLE “IoT Hardware Ready” allows quick and easy prototyping of IoT devices

#### Key Features
- 0 to 100% relative humidity range
- Supply voltage: 1.7 to 3.6 V
- Low power consumption: 2 μA @ 1 Hz ODR
- Selectable ODR from 1 Hz to 12.5 Hz
- High rH sensitivity: 0.004% rH/LSB
- Humidity accuracy: ± 3.5% rH, 20 to +80% rH
- Temperature accuracy: ± 0.5 °C,15 to +40 °C
- Embedded 16-bit ADC
- 16-bit humidity and temperature output data
- I²C interfaces
- Factory calibrated

## Step 1.1 Download & Install ST BLUEMS APP and connect SensiBLE

![](./images/Download_app.png)

After downloading the app insert battery into the SensiBLE. Red led should light up in SensiBLE. Open application and click **Connect to a device**. Select your **device** from list by clicking it. Now you should see data from your device and the led should be green. (_The application layout might be different using Android_)

![](./images/Connect_app_sensor.png)

Now your SensiBLE devices is connected to your phone. **When you close the app the connection closes and the led is red.** To reconnect open the app and bush the button in SensiBLE side.

# Step 2. Create Watson IoT Platform and connect SensiBLE

## Create Watson IoT Platform

In this section we are going to create a **_Watson IoT Platform_** instance on IBM Cloud, and use it to connect SensiBLE device to receive data.

**(1)** Log into IBM Cloud and create a **_Watson IoT Platform_** service.
- Click on `Catalog`, then filter by clicking on `Internet of Things`
- Select `Internet of Things Platform`

![](./images/IBM_Cloud_Catalog.png)

**(2)** Create the service with a unique name: we'd suggest something like `Internet of Things Platform-eventname-yourinitials`, e.g. `Internet of Things Platform-workshop-JH`

Ensure you are using the `Lite` plan.

![](./images/IBM_Cloud_IoT.png)

Scroll down and give the service name you want, then hit `Create`.

![](./images/IBM_Cloud_name_IoT.png)

**(3)** Click on `Launch`.

![](./images/IBM_Cloud_launch_IoT.png)

**(4)** You might need to sing in using your **IBM Cloud Username and Password**.

![](./images/Sign_in_IBM_IoT_platform.png)

**(5)** Click your name in upper right corner.

![](./images/IBM_IoT_platform.png)

**(6)** Select organization by clicking it.

![](./images/Platform_account.png)

#### **Now you are ready to connect your device. Nice work!**


## Connect SensiBLE to Watson IoT Platform

**(1)** Click `Add Device`.

![](./images/IBM_IoT_add_device.png)

**(2)** From ST BLUEMS APP you need to find Device Type and Device Id.

![](./images/Device_id_type.jpeg)

**(3)** Add Device Type and Device ID from App and click `Next`.

![](./images/IBM_IoT_add_device_id_type.png)

**(4)** Next you can add metadata but now we skip this part and click `Next`.

![](./images/Metadata.png)

**(5)** You can write your own **Authentication Token** example "Sensi2901" and click `Next`.

![](./images/IBM_IoT_Token.png)

**(6)** Now you can see summary of your device. Add **Organization** (from upper right corner, after ID: "This is organization") and **Authentication Token** (you just write it) information to the APP.

## **Kuva tähän vielä**

![](./images/IBM_IoT_Token.png)

If the information is correct click `Finnish`.

![](./images/Add_device_summary.png)

**(7)** Now you can click `Connect` from the APP and select Humidity and Temperature.

![](./images/Connect_select.png)

From IBM IoT Platform you can see in `Recent Events` section the data from SensiBLE.

![](./images/Recent_event.png)

**You have now connected SensiBLE to IBM IoT Platform. Good job!**

# Step 3. Create Node-Red dashboard and connect Watson IoT Platform for visualises data

# Summary

In this lab you created connection between SensiBLE and Watson IoT platform and visualised the data in a dashboard using Node-RED.
