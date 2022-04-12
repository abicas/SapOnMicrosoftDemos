+++
title = "Running the lab"
date = 2022-03-10T14:52:21-03:00
weight = 7
chapter = false
pre = "<b>3. </b>"
+++

In this step we will execute the Workflow created previously

Go back to Overview, Enable Debug mode (will be used in the future) and copy the Workflow URL provided
![Logic App](/images/logicapp27.png)

We need to invoke the API, so we can use an externall tool like Postman or use the embeded **Run Trigger** tool. 

For Postman: 
- Method: **POST** 
- URL: **copied on the previous step** 
- Body: **raw** - **JSON** 
- Body content: `{"id": "0000000728"}` or `{"id": "0000001575"}` 
    - Note: SAP compares strings so have that in mind with leading zeroes and 10 total chars
- Hit Send.
![Logic App](/images/logicapp28.png?height=500px)

For **Run Trigger** tool: 
1. Click on **Run Trigger with payload** 
![Logic App](/images/logicapp29.png?height=100px)
2. Fill the request: 
    - Method: **POST**
    - Content-Type: **application/json** 
    - Body content: `{"id": "0000000728"}` or `{"id": "0000001575"}` 
        - Note: SAP compares strings so have that in mind with leading zeroes and 10 total chars
    - Click Run 
![Logic App](/images/logicapp30.png)
3. When your workflow runs, you should receive an Output status = 200 
![Logic App](/images/logicapp31.png?height=300px)
4. You can see the run status on the **Run History** tab
![Logic App](/images/logicapp32.png)
5. And by selecting the desired Run, you can see step-by-step inputs and outputs of your workflow for debug.
![Logic App](/images/logicapp33.png)
6. For a sucessful Run you can also see the details and the time it took on every step: 
![Logic App](/images/logicapp34.png)

Now go check your email inbox because you should have something similar to the one below: 
![Logic App](/images/logicapp35.png)

If you need to check or compare a Sales Order on SAP, go to the Bastion Host via Remote Desktop, open SAP GUI and follow the steps below: 
- Logon with BPINST/Welcome1

Go to TCODE **VA03** (Display Sales Orders) 

Search for the order number used on VA03
- Order: **728** or **1575** (here SAP compared numbers and don't care about leading zeroes)
- Hit Search and you should see the details (to return to the previous screen, use the green arrow by the TCODE)
![Logic App](/images/logicapp36.png)


Congratulations ! You just finished the first lab and was able to create an API that will query SAP Sales Order and send an email, all with ZERO LINES of CODE ! 















