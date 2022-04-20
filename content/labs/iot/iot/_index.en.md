+++
chapter = false
pre = "<b></b>"
title = "Azure IoT & Logic Apps"
weight = 8
+++

### Azure IoT Hub

The Internet of Things (IoT) is a network of physical devices that connect to and exchange data with other devices and services over the Internet or other network. There are currently over ten billion connected devices in the world and more are added every year. Anything that can be embedded with the necessary sensors and software can be connected over the internet.

Azure IoT Hub is a managed service hosted in the cloud that acts as a central message hub for communication between an IoT application and its attached devices. You can connect millions of devices and their backend solutions reliably and securely. Almost any device can be connected to an IoT hub.

IoT Hub scales to millions of simultaneously connected devices and millions of events per second to support your IoT workloads. 

![IotHub](/images/iot-sample.png)

You can integrate IoT Hub with other Azure services to build complete, end-to-end solutions. For example, use:

- Azure Event Grid to enable your business to react quickly to critical events in a reliable, scalable, and secure manner.

- Azure Logic Apps to automate business processes.

- Azure Machine Learning to add machine learning and AI models to your solution.

- Azure Stream Analytics to run real-time analytic computations on the data streaming from your devices.

### What we will build

We will build a solution where a (virtual) IoT Device will send temperature and humidity data to Azure IoT Hub, which will trigger a Logic App. 

This Logic app will process each device telemetry message and if temperatura is greater than 29 degrees Celsius, it will generate an IDOC and send it to SAP. 

This could be used, for example, to mark a product defective or a batch of good produced marked for quality assurance. 

{{< youtube hXy4QTiIXh0 >}}

### Estimated Time for this Lab

This lab is estimated to take between 60 minutes.

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. Azure subscription