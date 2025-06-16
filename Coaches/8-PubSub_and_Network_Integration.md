# Pub/Sub and Network Integration

## Process Diagram

![Pub/Sub and VNet Integration Progress Diagram](images/pubsub-and-vnet-integration-progress-diagram.jpg)

## Overview

The primary objective of this challenge is to expose participants to the following concepts:

* Azure Functions Premium with virtual network integration
* Pub/Sub via Azure Service Bus topics and subscription filters (filtering events that need extra action)
* Messaging claim check pattern

## Happy Path

* Participant should create a new Service Bus topic to which to send messages.
* Modify the Azure Function used in the prior challenge to publish messages to a new Service Bus topic **only** if there is a ```receiptUrl``` in the data received from Event Hub.
    * Use the UserProperties of a Service Bus Message/BrokeredMessage type. The new property will need to have a key such as "TotalCost" and a value such as 134.59.  The property can be used by a Service Bus SQL filter for a subscription.
    * It is possible to use an output binding if using C#.
* Create two Service Bus subscriptions, one to handle all messages, and one to handle only messages where the total cost is greater than $100.  
* Create two functions (within the Functions Premium plan) to act as subscribers.  There should be one function per subscription.
* For the function which retrieves and base64 encodes the PDF:
    * use a Service Bus trigger to receive the message
    * use a blob output binding with [blob output binding for a random guid](https://docs.microsoft.com/azure/azure-functions/functions-bindings-expressions-patterns#create-guids) to set the file name
    * the receiptUrl should be a reference to an Azure storage blob using a SAS URL, and thus should be downloadable within the Azure function.
* Use the provided VM to view the files in Azure blob storage.  Remotely access the VM (using RDP) and then log into the Azure Portal (using the Azure credentials for the OpenHack).  Navigate to the Storage Explorer in the portal and then browse to view the files in blob storage.

## Coach's Notes

* VM (Jumpbox) Notes
    * *Username:* serverless
    * *Password:* ServerlessForAll2019
    * VM will automatically shut down at 19:00 UTC each day
* The following Azure resources should be provisioned in advance within the participant's Azure subscription:
    * 2 storage accounts
        * one for the VM's diagnostic data (storage account name should begin with 'sohvmdiag')
        * one for the storage of receipts (storage account name should begin with 'sohsales').  There should be two containers within this storage account: 'receipts' and 'receipts-high-value'
    * 1 Virtual Machine ('soh-jumpbox)
        * OS is Windows 10
        * VM uses a DevTestLab schedule to automatically shut down daily at 19:00 (no notification)
    * 1 Virtual Network ('soh-vnet')
        * 2 subnets
            * 'receipt-processing' - this is for use by the compute resource (ideally an Azure Functions Premium plan) used to process messages for this challenge
            * 'jumpbox' - this is for use exclusively by the VM
        * Subnets are configured with a virtual network service endpoint for access to Microsoft.Storage resources only.
        * 1 NSG to allow RDP access on port 3389

The diagram below depicts the Azure resources which are created for each team's Azure subscription.

![Azure resources](https://ohreleases.blob.core.windows.net/openhack-assets/serverlessimages/pubsub-and-network-challenge-existing-azure-resources.png)
