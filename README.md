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

## Download & Install ST BLUEMS APP and connect SensiBLE

![](./images/Download_app.png)

After downloading the app insert battery into the SensiBLE. Red led should light up in SensiBLE. Open application and click **Connect to a device**. Select your **device** from list by clicking it. Now you should see data from your device and the led should be green. (_The application layout might be different using Android_)

![](./images/Connect_app_sensor.png)

Now your SensiBLE devices is connected to your phone. **When you close the app the connection closes and the led is red.** To reconnect open the app and bush the button in SensiBLE side.

********************

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

**(5)** If you have multiple organization, click your name in upper right corner.

![](./images/IBM_IoT_platform.png)

**(6)** and select organization by clicking it.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/Platform_account.png" width="30%" height="30%">

#### **Now you are ready to connect your device. Nice work!**


## Connect SensiBLE to Watson IoT Platform

**(1)** Click `Add Device`.

![](./images/IBM_IoT_add_device.png)

**(2)** From ST BLUEMS APP you need to find Device Type and Device Id. The Device Type might be Nucleo but you can change it to SensiEDGE.

![](./images/Device_id_type.png)

**(3)** Add Device Type and Device ID from App and click `Next`.

![](./images/IBM_IoT_add_device_id_type.png)

**(4)** Next you can add metadata but now we skip this part and click `Next`.

![](./images/Metadata.png)

**(5)** You can write your own **Authentication Token** example "Sensi2901" and click `Next`.

![](./images/IBM_IoT_Token.png)

**(6)** Now you can see summary of your device. Open ST BLUEMS APP and add **Organization** (from upper right corner, after ID: "This is organization") and **Authentication Token** (you just write it) information into the APP.

![](./images/Add_Org_aut_token.png)

If the information is correct in Watson IoT Platform, click `Finnish`.

![](./images/Add_device_summary.png)

**(7)** Now you can click `Connect` from the APP and select Humidity and Temperature.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/Connect_select.png" width="60%" height="60%">

From IBM IoT Platform you can see in `Recent Events` section the data from SensiBLE.

![](./images/Resent_events.gif)

**You have now connected SensiBLE to IBM IoT Platform. Good job!**

**(8)** We need to create API Key and API Token for creating connection to Node-Red.

From left menu click `Apps`

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/IBM_IoT_Apps.png" width="30%" height="30%">

Click `Generate API Key`

![](./images/IBM_IoT_Generate_API.png)

Add information about the connection and click `Next`

![](./images/API_info.png)

Check role and click `Generate Key`

![](./images/API_role.png)

Here you can copy API Key and API Token. **After closing this you can't see the API Token anymore!**

![](./images/API_credentials.png)


******************************

# Step 3. Create Node-Red dashboard and connect Watson IoT Platform to visualize data

## Create Node-Red app from catalog

**About Node-RED**

Node-RED is a visual tool for wiring the internet of things - connecting hardware devices, APIs and online services in a new and interesting way. Node-RED provides a browser-based flow editor that makes it easy to wire together flows using the wide range nodes in the palette. Flows can be then deployed to the runtime in a single-click.

- JavaScript functions can be created within the editor using a rich text editor.
- A built-in library allows you to save useful functions, templates or flows for re-use.
- See [https://nodered.org](https://nodered.org) for more information.

**If you have running Node-Red application in IBM Cloud you can skip this and use that.**

**(1)** Go back IBM Cloud and create a **_Node-Red Cloud Foundry App_** service.
- Click on `Catalog`, write in search field **node-red** and click `Software`
- Select `Node-RED Starter`

![](./images/IBM_catalog_node-red.png)

**(2)** Click on the Create app button (1) to continue

![](./images/IBM_catalog_node-red-create-app.png)

**(3)** Now you need to configure the Node-RED Starter application.

1. On the *App details* page, a randomly generated name will be suggested – **Node RED SSLPD** in the screenshot below. Either accept that default name or provide a unique name for your application (1). This will become part of the application URL. _**Note:**_ If the name is not unique, you will see an error message and you must enter a different name before you can continue.

2. The Node-RED Starter application requires an instance of the Cloudant database service to store your application flow configuration. Select the region (2) the service should be created in and what pricing plan it should use. _**Note:**_ You can only have one Cloudant instance using the Lite plan. If you have already got an instance, you will be able to select it from the **Pricing plan** select box (3). You can have more than one Node-RED Starter application using the same Cloudant service instance.

3. Click the `Create button` (4) to continue. This will create your application, but it is not yet deployed to IBM Cloud.

![](./images/IBM_node-red_name.png)

**(4)** Enable the Continuous Delivery feature

At this point, you have created the application and the resources it requires, but you have not deployed it anywhere to run. This step shows how to setup the Continuous Delivery feature that will deploy your application into the **Cloud Foundry** space of IBM Cloud.

1. On the next screen, click the `Deploy your app` button (1) to enable the Continuous Delivery feature for your application.

![](./images/Deploy_your_app.png)

2. You will need to create an **IBM Cloud API** key to allow the deployment process to access your resources. Click the `New` button (1) to create the key. A message dialog will appear. Read what it says and then confirm and close the dialog.

3. The Node-RED Starter kit only supports deployment to the **Cloud Foundry** space of IBM Cloud. Select the `region` (2) to **deploy your application to**. This should match the region you created your Cloudant instance in.

4. Select the `region` (3) to create the **DevOps toolchain**.

5. Click `Create` (4). This will take you back to the application details page.

![](./images/NR-configure-pipeline.png)

6. After a few moments, the Continuous Delivery section will refresh with the details of your newly created Toolchain. The Status field of the Delivery Pipeline will show **In progress**. That means your application is still being built and deployed.

7. Click on the `In progress` link to see the full status of the Delivery Pipeline.

![](./images/NR-continuous-delivery.png)

8. The Deploy stage will take a few minutes to complete. You can click on the `View logs and history` link to check its progress. Eventually the Deploy stage will go green to show it has passed. This means your Node-RED Starter application is now running.

![](./images/NR-pipeline.png)

**(5)** Open the Node-RED application

Now that you’ve deployed your Node-RED application, let’s open it up!

1. Open your IBM Cloud Resource list by selecting the sidebar menu (1) and then selecting `Resource List` (2).

![](./images/ResourceList.png)

2. You will see your newly created Node-RED Application listed under the **Apps** section (1). You will also see a corresponding entry under the Cloud Foundry apps section (2). Click on this **Cloud Foundry app** entry to go to your deployed application’s details page.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/NR-resource-list.png" width="30%" height="30%">

3. From the details page, click the `Visit App URL` link to access your Node-RED Starter application.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/NR-app-details.png" width="50%" height="50%">


**(6)** Configure your Node-RED editor.

The first time you open your Node-RED app, you’ll need to configure it and set up security.

1. In this section, you will set up a username and password to protect your flow. Click `Next`.

![](./images/node-red_instance_setup.png)

2. Write an username and a password of your choice and click `Next`. Remember that it does not have to be related to your IBM Cloud access.

![](./images/node-red_instace_credits.png)

3. Node-RED is an open source project so you can add new nodes to the palette by modifying the package.json file. Click `Next`.

![](./images/node-red_instance_next.png)


![](./images/node-red_instance_finish.png)

**Your Node-RED flow is all set!**

**(7)** Now click `Go to your Node-RED flow editor` to open the flow editor and enter your credentials to access the editor.

![](./images/node-red_editor.png)

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/node-red_editor_credits.png" width="50%" height="50%">

The Node-RED editor opens showing the default flow.

![](./images/NR-editor.png)

When using Node-RED we build our apps using this graphical editor interface to wire together the blocks we need. We can simply drag and drop the blocks from the left menu into the workspace in the center of the screen and connect them to create a new flow.

Note: If you get an "Authorization denied" message when deploying your applications make your sure you are logged in. Click on the icon on the top right side of the Node-RED canvas and login with the credentials you created in the previous steps.

![](./images/node-red_signin.png)


## Build your Node-RED flow to show IoT data Dashboard

**(1)** Add extra nodes to your Node-RED palette

Node-RED provides the palette manager feature that allows you to install additional nodes directly from the browser-based editor. This is convenient for trying nodes out, but it can cause issues due to the limited memory of the default Node-RED starter application.

The recommended approach is to edit your application’s package.json file to include the additional node modules and then redeploy the application.

This step shows how to do that in order to add the [node-red-dashboard](https://flows.nodered.org/node/node-red-dashboard) module and [node-red-contrib-scx-ibmiotapp](https://flows.nodered.org/node/node-red-contrib-scx-ibmiotapp).

1. On your application’s details page, click the url in the **Continuous Delivery** box. This will take you to a git repository where you can edit the application source code from your browser.

![](./images/NR-continuous-delivery-url.png)

2. Scroll down the list of files and click on `package.json`. This file lists the module dependencies of your application.

![](./images/NR-file-list.png)

3. Click the `Edit` button

![](./images/NR-edit-file-button.png)

4. Add the following entry to the top of the dependencies section (1):

```
"node-red-dashboard": "2.x",
"node-red-contrib-scx-ibmiotapp": "0.x",
```

_**Note:**_ Do not forget the comma (,) at the end of the line to separate it from the next entry.

Add a **Commit message** (2) and click `Commit changes` (3)

![](./images/add_nodes.png)

5. At this point, the Continuous Delivery pipeline will automatically run to build and deploy that change into your application. If you view the Delivery Pipeline you can watch its progress. The Build section shows you the last commit made (1) and the Deploy section shows the progress of redeploying the application (2).

![](./images/Changes_and_status.png)

6. Once the Deploy stage completes, your application will have restarted and now have the node-red-dashboard nodes preinstalled.

If the nodes are not showing in Node-red. Refresh browser. You might need to login to your application.

<br>
**Congratulations!** You have now created a Node-RED application that is hosted in the IBM Cloud. You have also learned how to edit the application source code and automatically deploy changes.

<br>
<br>

**(2)** In order to make the lab easier we are going to import the rest of the code.

You can get the complete Node-RED flow from the **Hamk-IoT-Dashboard.json**.

Import the flow by simply clickcing on the 3 white lines on the top right corner of the Node-RED window. Click `Import` and paste the text you copied from above. Click `Import`.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/import_json.png" width="30%" height="30%">

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/paste_json.png" width="60%" height="60%">

Now your flow should look like this:

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/flow.png" width="70%" height="70%">


**(3)** Add information to IoT-node connecting IBM IoT Platform to Node-Red.

You will need to do some editing on IoT node, because credentials are not transferred with the rest of the code. Edit the blue IBM IoT node with:
- your own credentials (API Key and API Token from IBM IoT Platform)
- change SensiBLE Device Id correct one (you can find this from IBM IoT Platform or from ST BLUEMS APP)

Bouble-click IBM IoT node

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/IBM_IoT.png" width="30%" height="30%">

Change Device Id and click pen icon next to API Key

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/IBM_IoT_change.png" width="60%" height="60%">

Add copied API Key and API Token from IBM IoT Platform. Click `Update`.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/IBM_IoT_API_credentials.png" width="60%" height="60%">

When you have make all the changes to this node, click `Done`.

**(4)** Add voice alarm

From list drag function-node and audio out -node. Connect them by clicking grey box and drag connection to another node.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/voice_alarm.png" width="60%" height="60%">

Double-click function node and add code:

```
if (msg.payload.d["Temperature"] >= 30){
    msg.payload = "Lämpötila koholla";
    return msg;
}

if (msg.payload.d["Humidity"] >= 60){
    msg.payload = "Ilmankosteus koholla";
    return msg;
}
```
This code makes voice alarm when temperature is/or is above 30 degree and when humidity is/or is above 60 degree. You can change these if you want. The alarm is written in Finnish Language but you can change it to something else.

Double-click voice audio -node and select voice you want to use and select the Group your dashboard name [IoT Dashboard] Temperature. If you don't select the Group Node-RED don't know which it belongs to and it won't work.

Now add the connection from IBM IoT -node to function-node. Your flow should look like this.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/flow_voice_alarm.png" width="60%" height="60%">



**(5)** View Dashboard UI
Now, first click `dashboard-button` from upper right corner and then click `Deploy`. Everytime `Deploy` is red there are changes in the flow that has not been update. Next click link to access ui.

<img src="https://github.com/jenni-hautojarvi/Watson-IoT-Lab/blob/master/images/link_to_dashboard.png" width="50%" height="50%">

New Tab opens and now you can see your data from SensiBLE in Node-Red Dashboard.

![](./images/Dashboard.png)

If there is no data flow:
- Check that your devices is connected to mobile App
- Check from IBM IoT Platform Device Event part that you are receiving data. There should be continues data flow.
- Check from Node-Red debug (button next to dashboard button) that you are receiving data.


# Summary

In this lab you created connection between SensiBLE and Watson IoT platform and visualised the data in a dashboard using Node-RED.
