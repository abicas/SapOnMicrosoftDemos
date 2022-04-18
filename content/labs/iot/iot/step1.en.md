+++
chapter = false
pre = "<b></b>"
title = "IoT Hub Setup"
weight = 7
+++

Before we start sending data to SAP, we need to create an IoT Hub to receive the ioT telemetry data and process it as it arrives. 

This section will show the steps required to prepare the environment for that:

### Setting up Azure IoT Hub

1. Log on to the [Azure Portal](https://portal.azure.com) and look for **Iot Hub**
![iot](/images/iot01.png?height=150px) 
2. On IoT Hub page, select **Create** 
![iot](/images/iot02.png?height=150px) 
3. Provide the required information. Select the same region that SAP was deployed:
- Resource Group: **IotRG** (create new RG)
- IoT Hub Name: **SAPIOTLAB** (must be unique on Azure)
- Region: **East US** 
- Click: **Next: Networking>** 
![iot](/images/iot03.png?height=550px) 
4. Make sure we have Public Access setup so we can send data via internet. Click: **Next: Management>** 
![iot](/images/iot04.png?height=550px) 
5. For this lab, we can use the Free Tier to accomplish our goals. FRee Tiear can scale up to 8k messages/day. Click: **Review + create** 
![iot](/images/iot05.png?height=550px) 
6. Check the values and click: **Create** 
![iot](/images/iot06.png?height=550px) 

### Creating our IoT Device

For this lab we will use a virtual Raspberry Pi Emulator. It runs virtually the same code you can run on a physical device, making it simple for us to show the conectivity and data flow, without having to play with electronics. 
![iot](/images/iot-sample01.png) 

7. In the Newly created Iot Hub, select **Devices** on the left panel and click **Add Device** 
![iot](/images/iot07.png?height=550px) 
8. Name it **VirtualRapberryPi** and make sure the defaults are like the picture. Click **Create** 
![iot](/images/iot08.png?height=550px) 
9. Once created, you can see the device under the Devices panel. Click on the **VirtualRaspberryPi** device.
![iot](/images/iot09.png) 
10. Here we will copy the **Primary Connection String** so the virtual device can communicate and authenticate with Azure. 
![iot](/images/iot10.png)

### Configuring the Raspberry Pi Azure IoT Simulator

As described before we will use a virtual device to run this lab. This device is a very simple one with an LED and a temperature/humidity sensor that will measure and send to Azure IoT Hub the most recent data. 

11. Go to the [Raspberry Pi Azure IoT Online Simulator](https://azure-samples.github.io/raspberry-pi-web-simulator/). The app has 3 parts: The device diagram (1), the code (2) and the control section (3) where we can command the device and see the messages. 
![iot](/images/iot-sample02.png) 
12. On the Code section, we need to provide the credentials for our IoT Hub. Replace the **[Your IoT Hub device connection string]** with the copied **Primary Connection String**. Make sure you leave the quotes around the Connection String.  
![iot](/images/iot11.png)
13. Make sure your lab is similar to the example and click **Run** to test it. 
![iot](/images/iot12.png)
14. If everything is correct, you will see messages being sent to Azure IoT Hub. Message are in JSON format. 
![iot](/images/iot13.png)
15. Back on the device page on Azure portal, click on **Message to Device** so we can send some data from the cloud to the device
![iot](/images/iot14.png)
16. Use the message template below and click **Send Message** 
`{"messageId": 99, "deviceId": "Raspberry Pi Web Client", response: "Hello from Iot Hub!"}`
![iot](/images/iot15.png)
17. Check back the Simulator console for the recently sent message:
![iot](/images/iot16.png)
18. In order to see the messages sent from the device, you can check the **Overview** on the left panel on the IoT Hub. Once we just started sending data, click on **1 Hour** so we can zoom in the charts:  
![iot](/images/iot17.png)
19. To see the messages being sent, open an **Cloud Shell** from the top icon. Select **BASH** and run the following command to stream the data: 
`az iot hub monitor-events --hub-name SAP IOTLAB`
![iot](/images/iot18.png)

Congratulations ! You have setup the Azure IoT Hub and the Device is communicating properly. 

On the next section we will build a Logic App that will consume this data and depending on the parameters received, send data to SAP. 





