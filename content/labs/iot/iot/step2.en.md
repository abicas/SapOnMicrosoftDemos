+++
chapter = false
pre = "<b></b>"
title = "Building the LogicApp"
weight = 9
+++

Let's build a Logic App to consume the data and decide if this should be sent to SAP or not. 

1. Log on to the [Azure Portal](https://portal.azure.com) and look for **Logic Apps**
![iot](/images/iot-a-19.png?height=150px)
2. Create a new logic app with the following parameters: 
- Resource Group = **IoTRG** (created on the previous step)
- Logic App Name = **SAPIOTLABXXXX** (must be unique on Azure. Replace XXXX with a set of 4 numbers, like SAPIOTLAB1234)
- Region = **East US** 
- Click on **Review + create**
![iot](/images/iot-a-20.png?height=400px)
3. Once the logic app is created, go to the **Events** on the left panel and select **Logic Apps** 
![iot](/images/iot-a-22.png?height=400px)
4. The Logic Apps Designer will open with an Azure Event Grid setup. Confirm the Active Directoy to be used, click Sign In and log in with your credentials. 
![iot](/images/iot-a-23.png?height=400px)
5. Once logged in, you will see a green checkmark. Click **Continue** 
![iot](/images/iot-a-24.png?height=300px)
6. Let's configure the Source event. configure the parameters as below and click on **Next Step** 
- Resource Type = **Microsoft.Devices.IoTHubs** 
- Resource Name = Should be already populated, if not select your SAPIOTLAB IoT Hub 
- Event Type = **Microsoft.Devices.DeviceTelemetry** 
![iot](/images/iot-a-25.png?height=400px)
7. Search for **Parse JSON** and select **Parse JSON** as the next step
![iot](/images/iot-a-26.png?height=400px)
8. In Content, use dynamic content and select **Body** from "When a resource event occurs". Click on **Use payload to generate schema** 
![iot](/images/iot-a-27.png?height=400px)
9. Paste the sample payload below and click **Done**
```json
{	
	"id": "<Telemetry ID>",
    "topic": "/SUBSCRIPTIONS/<Suscription ID>/RESOURCEGROUPS/RG-AZUREIOT/PROVIDERS/MICROSOFT.DEVICES/IOTHUBS/ELBRUNOIOT",
	"subject": "devices/wioSquirrelFeeder",
	"eventType": "Microsoft.Devices.DeviceTelemetry",
	"data": {
	"properties": {},
	"systemProperties": {
	"iothub-connection-device-id": "wioSquirrelFeeder",
	"iothub-connection-auth-method": "{\"scope\":\"device\",\"type\":\"sas\",\"issuer\":\"iothub\",\"acceptingIpFilterRule\":null}",
	"iothub-connection-auth-generation-id": "637769331872294921",
	"iothub-enqueuedtime": "2022-03-02T15:27:08.4210000Z",
	"iothub-message-source": "Telemetry"
	},
	"body": "eyJhY3Rpb24iOiJhbmltYWwgZGV0ZWN0ZWQiLCJhbmltYWwiOiJzcXVpcnJlbCIsImZlZWRjb3VudCI6OCwiZmVlZGVyX3N0YXRlIjpmYWxzZSwicmFuZ2VfZGV0ZWN0ZWQiOjM3fQ=="
	},
	"dataVersion": "",
	"metadataVersion": "1",
	"eventTime": "2022-03-02T15:27:08.421Z"
}
```
![iot](/images/iot-a-28.png?height=300px)
10. Add a new step after Parse JSON. 
![iot](/images/iot-a-29.png?height=400px)
11. As you can see on the template above, the body for the document is base64 enconded. We need to convert it to string so we can handle the values sent by the device. Let's add a **Compose** operation to convert this format: 
![iot](/images/iot-a-30.png?height=400px)
12. On the **Inputs** field, we will use use dynamic content. Click on **Expression** and paste the expression below. Click **OK** 
`decodeBase64(string(body('Parse_JSON')?['data']?['body']))`
![iot](/images/iot-a-31.png?height=400px)
13. Add another **Parse JSON** step, and rename it to **Parse BODY**. 
![iot](/images/iot-a-32.png?height=250px)
![iot](/images/iot-a-33.png?height=170px)
14. On Parse Body, select content and add the Dynamic content **Outputs** from the previous Compose step. Click on **Use payload to generate schema** 
![iot](/images/iot-a-34.png?height=400px)
15. Paste the sample payload below and click **Done**
```json
{
    "messageId":5,
    "deviceId":"Raspberry Pi Web Client",
    "temperature":24.663457932335028,
    "humidity":65.91259670696867
}
```
16. Now we can read the data sent by the device. Let's add the IF/THEN decision in the flow. Add a new step **Condition** (you can search for control)
![iot](/images/iot-a-35.png?height=400px)
17. Let's define that temepratures above 29oC should trigger the IDOC to SAP to alert it. Add the field **temperature** from Parse Body... 
![iot](/images/iot-a-36.png?height=400px)
18. ... and as condition select **is greater than** and **29** . CLick on **Add Action** under the True result. 
![iot](/images/iot-a-37.png?height=300px)
19. Inside the True result, add a new **Compose** step 
![iot](/images/iot-a-38.png?height=300px)
20. Rename it to **Build XML** 
![iot](/images/iot-a-39.png?height=300px)
21. As input, paste the XML Template below. This is a sample IDOC tempalte from SAP for flight data. Although it has nothing to do with your example, our focus is not about configuring the SAP side but instead focus on transmitting the message to SAP. This IDOC is already defined on SAP and ready to be used, which fits our objectives. 
We will replace the 3 **XXX** values with Dynamic Content as the picture below
- AGENCYNUM = **messageId**
- PASSNAME = **temperature**
- PASSBIRTH = **humidity**
- Make sure you do not leave spaces before or after the dynamic values
```xml
<?xml version="1.0" encoding="UTF-8" ?>
<FLIGHTBOOKING_CREATEFROMDAT01>
	<IDOC BEGIN="1">
		<EDI_DC40 SEGMENT="1">
			<TABNAM>EDI_DC40</TABNAM>
			<MANDT>000</MANDT>
			<DOCREL>750</DOCREL>
			<STATUS>56</STATUS>
			<DIRECT>2</DIRECT>
			<OUTMOD/>
	<IDOCTYP>FLIGHTBOOKING_CREATEFROMDAT01</IDOCTYP>
			<CIMTYP/>
			<MESTYP>FLIGHTBOOKING_CREATEFROMDAT</MESTYP>
			<SNDPOR>A000000002</SNDPOR>
			<SNDPRT>LS</SNDPRT>
			<SNDPRN>S4HCLNT100</SNDPRN>
			<RCVPOR>A000000002</RCVPOR>
			<RCVPRT>LS</RCVPRT>
			<RCVPRN>S4HCLNT100</RCVPRN>
			<CREDAT>20191001</CREDAT>
			<CRETIM>090207</CRETIM>
		</EDI_DC40>
		<E1SBO_CRE SEGMENT="1">
			<RESERVE_ONLY>X</RESERVE_ONLY>
			<TEST_RUN>X</TEST_RUN>
			<E1BPSBONEW SEGMENT="1">
				<AIRLINEID>AA</AIRLINEID>
				<CONNECTID>1234</CONNECTID>
				<FLIGHTDATE>01012022</FLIGHTDATE>
				<CUSTOMERID>00001234</CUSTOMERID>
				<CLASS>B</CLASS>
				<COUNTER>ALERT</COUNTER>
				<AGENCYNUM>XXX</AGENCYNUM>
				<PASSNAME>XXX</PASSNAME>
				<PASSBIRTH>XXX</PASSBIRTH>
			</E1BPSBONEW>
			<E1BPPAREX/>
		</E1SBO_CRE>
	</IDOC>
</FLIGHTBOOKING_CREATEFROMDAT01>
```
![iot](/images/iot-a-40.png)
22. Finally, still inside the True result and under Build XML, let's add the last step so we can send data to SAP. Filter for **message to SAP** and select **Send message to SAP**
![iot](/images/iot-a-41.png?height=400px)
23. We will need to configure the connection to SAP. use the following parameters: 
- Connection Name = **S4HANA** 
- Data Gateway = Your subscrition and the gateway name you picked on the environment setup. 
- Client = **100** 
- Authentication Type = **Basic** 
- SAP Username = **BPINST** 
- SAP Password = **Welcome1** 
- AS Host = **Your SAP HANA Public IP address** as displayed in SAP CAL
- AS Service = **50000**
- AS System Number = **00** 
- Leave the remaining parameters as the default 
![iot](/images/iot-a-45.png)
24. Under SAP Action we will define the IDOC template FLIGHTBOOKING_CREATEFROMDAT. In order to to this, click on the folder icon and on the arrow next to **IDOC** 
![iot](/images/iot-a-46.png)
25. Navigate on all the available IDOCs until **FLIGHTBOOKING_CREATEFROMDAT** is found and click on the arrow. 
![iot](/images/iot-a-47.png?height=300px)
26. Again click on the arrow for the single item: 
![iot](/images/iot-a-48.png)
27. Scroll down to the last option. It should be version 755 or above. hover the mouse to the name and wait for the pop up to confirm. Click on the arrow. 
![iot](/images/iot-a-49.png)
28. Finally select **SEND** as the action itself. 
![iot](/images/iot-a-50.png)
29. In **Input Message** set **Outputs** as dynamic content from BUILD XML step 
![iot](/images/iot-a-51.png)
30. Click **SAVE**
![iot](/images/iot-a-52.png)

Allright, we have created an LogicApp to handle the input from the IoT Device and send it to SAP in case temperaature is higher than 29oC. 

On the next step we will test it and check on the SAP side for the message that can be later handled but ABAP code. 






