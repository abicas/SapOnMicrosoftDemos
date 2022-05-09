+++
title = "Azure Data Factory"
date = 2022-03-14T14:13:05-03:00
weight = 5
chapter = false
pre = "<b></b>"
+++

### Azure Data Factory

In the world of big data, raw, unorganized data is often stored in relational, non-relational, and other storage systems. However, on its own, raw data doesn't have the proper context or meaning to provide meaningful insights to analysts, data scientists, or business decision makers.

Big data requires a service that can orchestrate and operationalize processes to refine these enormous stores of raw data into actionable business insights. Azure Data Factory is a managed cloud service that's built for these complex hybrid extract-transform-load (ETL), extract-load-transform (ELT), and data integration projects.

Azure Data Factory is Azure's cloud ETL service for scale-out serverless data integration and data transformation. It offers a code-free UI for intuitive authoring and single-pane-of-glass monitoring and management. 

![ADF2](/images/adf-sample1.png?height=300px)

### Extracting SAP DATA with Azure Data Factory

You can copy data from SAP ECC and SAP BW to any supported sink data store. Specifically, the SAP ECC connector supports:

![ADF2](/images/adf-sample.jpg?height=200px)

- Copying data from SAP ECC on SAP NetWeaver version 7.0 and later.
- Copying data from any objects exposed by SAP ECC OData services, such as:
    - SAP tables or views.
    - Business Application Programming Interface [BAPI] objects.
    - Data extractors.
    - Data or intermediate documents (IDOCs) sent to SAP Process Integration (PI) that can be received as OData via relative adapters.
- Copying data by using basic authentication.

![ADF2](/images/adf-sample2.png?height=400px)

### What we will build

In this lab we will prepare Azure Data Factory (ADF) to connect to SAP and then extract the Materials master data to a file to a Blob in our datalake. 

The video below shows an example of what we will do, creating a simple ADF pipeline to extract SAP data (and directly from SAP HANA as well, run it on-demand, and checking the file content that was exported to a blob storage. 

{{< youtube jDR5jbqMktw >}}

### Estimated Time for this Lab

This lab is estimated to take around 30 minutes.

### Requirements

For this demo we will be using the following components from the Environment Setup: 

1. S/4HANA deployed from SAP CAL
2. On-premises data gateway installed and configured 
3. Azure subscription