# Process POS sales events

## Progress Diagram

![Process POS sales event progress diagram](../images/process-pos-sales-event-progress-diagram.jpg)

## Happy Path

* Event Hub trigger for Azure Function
* Function trigger changed to receive a batch (string[] in C#)
* Host.json changed to match requirements
* App insights query for role instance count per minute

## Coaches Notes

* Need to set ‘"cardinality": "many" for JavaScript Azure Functions to enable batch receives

* When posting to register the event hub, the team should use a unique table number.  The API for post can be found [here](https://petstore.swagger.io/?url=https://serverlessohmanagementapi.azurewebsites.net/api/definition).  What matters is that the team table number is unique, such as seattle-table-1 or london-table-8.  This should be the same table number that the team used in the previous challenge, and should be unique per table/team.  Additionally, if the team failed to register their storage account, it is likely the event hub will not register.  Please make sure to let them know they must have registered their storage account.  Some people will skip or defer that step due to the amount of traffic it generates to the storage account (or they will disconnect the storage account, also breaking the flow of this open hack because it will de-register their table).

* Be prepared to discuss the impact of setting the function app's ```maxBatchSize``` to 64 and ```prefetchCount``` to 256.  There is nothing special about those numbers.  They're a starting point.  Attendees should use those and observe performance and scalability. As a coach, you should discuss how to process messages within the batch, including error/exception handling.  

    More information regarding functions:

    * [Sample host.json file](https://docs.microsoft.com/en-us/azure/azure-functions/functions-host-json)

    * [Host.json - Functions Bindings to Event Hubs](https://docs.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs-trigger?tabs=csharp#hostjson-properties)  

        >Note: Functions on version 1 use a different configuration, but this should not be in play for new development

    * [Functions Binding to Event Hubs](https://docs.microsoft.com/azure/azure-functions/functions-bindings-event-hubs)

    * [Azure Functions Best Practices](https://docs.microsoft.com/en-us/azure/azure-functions/functions-best-practices)  

    * [Azure Functions and Event Hubs: Optimizing for Throughput](https://medium.com/@iizotov/azure-functions-and-event-hubs-optimising-for-throughput-549c7acd2b75)  

    * [Understanding Event Processor Host in Azure Event Hubs](https://channel9.msdn.com/Shows/On-NET/Understanding-the-Event-Processor-Host-in-Azure-Event-Hubs)

* Preference is for them to have their function apps under with Consumption plan, not App Service Plan (easier to show the auto scale). If they didn’t, take them through setting up auto scale for App Service Plan with a low scale up measurement (like 10% CPU).

* Prompt attendee to view server count **before** turning on boost mode (so they can see the default vs. functions scaling).

* To get the number of active servers for a specific function, use either the Application Insights Live Metrics view, or a Log Analytics query, such as the following:

    ```sql
    requests
    | where name == "ProcessSalesEventBatch"
    | summarize count() by cloud_RoleInstance  
    | summarize count()
    ```

* If working with a Python Function app, Live Metrics does **not** show the correct number of servers which the function app has scaled out to (always shows 1). This is a [known issue](https://github.com/Azure/azure-functions-python-worker/issues/35). Instead, retrieve the number of active instances by using a Log Analytics query, such as the following:

    ```sql
    requests
    | where operation_Name  == ""
    | distinct cloud_RoleInstance
    | count
    ```

* View configuration in host.json to validate batch and prefetch count.

* If using Cosmos DB, ensure the RUs are high enough to handle the throughput (otherwise requests may get throttled).
    * [Request Units in Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/request-units)
    * [Estimate RU/s using the Azure Cosmos DB capacity planner](https://docs.microsoft.com/azure/cosmos-db/estimate-ru-with-capacity-planner)

## Challenge Steps:

### Step 1: Create an Event Hubs Namespace and Event Hub

1. Naviget to Azure Portal, search for **Event Hubs** and click on **Create** with the following settings:

   - Select serverless-openhack as Resource Group
   - Provide a unique Namespace Name
   - Keep the Pricing Tier as Standard
   - Click on **Review + Create** then **Create**.

1. Once the namespace is deployed, navigate to the namespace, **+ Event Hub**  and create an **Event Hub**.

1. Provide a unique name and set Partitions to 32.

1. Leave the Message Retention default and click on **Create**.

### Step 2: Get the Connection String with Send Permissions

1. Go to your **Event Hubs Namespace > Shared Access Policies > RootManageSharedAccessKey** (or create a new policy with Send permissions).

1. Copy the Primary Connection String.

1. Make sure it’s namespace-level, not Event Hub-level.

1. Note down the Event Hub Name you created in a notepad.

### Step 3: Register Event Hub with OpenHack API

1. Make a POST call to /team/registerEventHub with:

    - teamTableNumber: Your team table number
    - eventHubConnectionString: Primary Connection string
    - eventHubName: Event Hub Name

1. Example POST body:

   ```
   {
      "teamTableNumber": 5,
      "eventHubConnectionString": "<your_connection_string>",
      "eventHubName": "possales"
   }
   ```

1. This will enable the POS system to start sending events to your Event Hub.

### Step 4: Create an Azure Function App to Process POS Events

1. In Azure Portal, search Function App and click on **Create** with the following settings:

    - Select serverless-openhack as the Resource Group
    - Provide an unique Function App Name
    - Select the preferred Runtime Stack: .NET / Node.js / Python
    - Plan: Consumption (Serverless)
    - Click on **Review + Create > Create**.

### Step 5: Add Event Hub Trigger Function

1. Go to your Function App, **Functions** and **+ Add > Event Hub trigger** with the following settings:

    - Function Name: ProcessSalesEvents
    - Event Hub Connection: create a new connection and paste the namespace-level connection string
    - Event Hub Name: possales
    - Consumer Group: $Default

### Step 6: Implement Event Processing and Test the function

1. Inside the Function code:

   - Loop through each event in the batch.
   - Parse the JSON payload.
   - Store one entry per sale event in your database (CosmosDB or SQL).
   - Handle receiptUrl which can be null.

1. Example pseudocode in Node.js:

   ```
   module.exports = async function (context, eventHubMessages) {
     for (const event of eventHubMessages) {
        const sale = JSON.parse(event);
        // Insert sale into CosmosDB collection
        await cosmosClient.database("bfyoc").container("sales").items.create(sale);
     }
   };
   ```

1. Trigger POS events using OpenHack API.

1. Verify that the:

   - Azure Function receives batches
   - Debatches each sale event
   - Inserts into your database correctly
