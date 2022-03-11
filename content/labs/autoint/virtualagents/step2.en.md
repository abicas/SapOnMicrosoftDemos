+++
title = "Testing our Chatbot"
date = 2022-03-10T17:25:38-03:00
weight = 6
chapter = false
pre = "<b>2. </b>"
+++
In this section we will test and debug our Chatbot on Microsoft Power Platform. 

On the left side of the screen go to the Test bot and simulate a user conversation. 
- IMPORTANT: 
    - SAP expects a 10 char stirng with leading zeroes, so if you want to check order 728 you need to type **0000000728** 
    - Once we are doing a lab, we are not treating the input so type just the PO number with no other information, leading/trailing spaces, words, once we are passing the whole input to SAP. In a production bot more data treatment should be done, by creating a regexp and defining an Entity. 
![VA](/images/va17.png?height=450px) 

We should see the String we created on the Flow. Don't worry with the format now, on Teams it will render as a table. 
![VA](/images/va18.png?height=450px) 

If you need to debug the Flow, click on **View flow details** 
![VA](/images/dva01.png?height=450px) 

It will show all the flow runs and clicking on a run, will give you details step-by-step as well as more information for debug. 
![VA](/images/dva02.png?height=450px) 

Sucessful Run Example: 
![VA](/images/dva04.png?height=400px) 

Failed Run Example:

In this example I was logged on SAP GUI on exactly the required item, so I accidentally generated a lock that prevented the bot to query the data. Closing SAP GUI solved it. 
![VA](/images/dva03.png?height=400px) 




