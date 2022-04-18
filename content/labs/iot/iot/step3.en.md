+++
chapter = false
pre = "<b></b>"
title = "Testing the lab"
weight = 10
+++

Let's build a Logic App to consume the data and decide if this should be sent to SAP or not. 

1. Go to the [Raspberry Pi Azure IoT Online Simulator](https://azure-samples.github.io/raspberry-pi-web-simulator/) and click **Run**. Once you see a couple of messages with temperature above 29oC, click **Stop**
![iot](/images/iot-a-53.png)
2. On the Logic Apps page, go to **Overview** and check the **Runs history** for the executions. Each message should have executed the flow once. 
![iot](/images/iot-a-54.png)
3. If you click on the run itself, it will present all the detais of inputs and outputs of every step in the flow. This is useful for debugging in case your run failed. 
![iot](/images/iot-a-54b.png)
4. On the SAP Bastion Host, via Remote Desktop, open SAP GUI and go to TCODE **WE02**
![iot](/images/iot-a-55.png)
5. Accept the defaults (new idocs created from midgnith until now) and click on the **Run** icon. Adjust the values if needed to math the current date. 
![iot](/images/iot-a-56.png)
6. Here you can see all the IDOCs received. Double click the last one. 
![iot](/images/iot-a-57.png)
7. Open **Data Records**, then open **E1SBO_CRE** and double click on the **E1SBONEW**. You will see the XML content as IDOC. Look at the AGENCYNUM, PASSNAME and PASSBIRTH values that were replaced by the same values sent by the device. 
![iot](/images/iot-a-59.png)
![iot](/images/iot-a-58.png)

Congratulations! You just automated the data flow from an IoT device directly to SAP via Azure Logic Apps. 