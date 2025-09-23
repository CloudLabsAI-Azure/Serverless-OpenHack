# Create your first serverless function & workflow

## Happy path

One of these three directions used:​

* Use latest Visual Studio with the latest Functions and Webjobs Extension to create the function app & the functions, test locally and to publish to Azure

* Use Visual Studio Code with the latest Azure Functions Extension to create the function app, the functions, test locally, and to publish to Azure

* Use (Java/Python) favorite IDE with latest Azure Functions Core Tools and Azure CLI to create the function app, the functions, test locally, and to publish to Azure

## Python developer notes

* VS Code users can use the [Functions Extension](https://docs.microsoft.com/azure/python/tutorial-vs-code-serverless-python-05) to deploy the Function app, but will abstract from the developers what is occurring during the deployment. Encourage the developers to use the [Azure Function Core tools](https://docs.microsoft.com/azure/azure-functions/functions-reference-python#publishing-to-azure) for the deployment. This will give them greater visibility into the remote build occurring in the cloud.

## Coaches Notes

* This is the only challenge that has requirements that are individual; all others they will need to work together, or split into sub-teams then share the lessons and merge the work​

* Support and guide each team member throughout the setup process (Visual Studio, VS Code, dependencies, etc.) and questions they might have about Functions and Logic Apps​

* Spend some time to explain how this challenge is mostly about level setting (basically a Challenge 0), and gives them an intro to Functions and Logic Apps; and that the rest of the challenges will give them a better business and technical idea of serverless​

* Make sure the result is correct; that they are calling the function using GET and the Logic App using POST​

* Feel free to explain the different options for creating a function locally, steer them towards VS Code and VS if possible unless they really want to try something themselves that isn't C# or Node (like Java or Python)

* Make sure they have the latest versions VS and of the extensions​

* VS Code is finicky if you don’t have the right version of the functions runtime or .NET Core (uninstall all .NET core and install the latest SDK fixes things, and also installing the latest runtime)​
* If using the Logic Apps extension in VS Code, please note that the designer is _read-only_.  The VS Code [extension page](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-logicapps) shows (animated GIF) that the designer is read-only.  For a full graphical editing experience, use Visual Studio or the Azure Portal.

* Careful when installing the functions core tools using chocolatey, it seems to install the 32 bit version of it that has a bug​

* If using node with functions, make sure the node version in app settings for the function is set to at least 8.4.0.  Ideally, this would match your current node version (such as v12).

* Runtime and Nuget Packages that work well:

Product | Version
------- | -------
Visual Studio | 16.3.2
Functions and WebJobs Extension for VS | V15.0.40502
.Net Core SDK | [.Net Core](https://dotnet.microsoft.com/download/visual-studio-sdks)
Function Core Tools | 2.7.1633
Other nuget libraries | ...
Microsoft.ApplicationInsights | 2.11.0
Microsoft.NET.Sdk.Functions | 1.0.28
CsvHelper | 12.1.2
Microsoft.Azure.WebJobs.Extension.CosmosDB | 3.0.3
Microsoft.Azure.WebJobs.Extensions.DurableTask | 1.8.2
Microsoft.Azure.WebJobs.Extensions.EventHubs | 3.0.3

## Step 1: Create and Debug Your First HTTP Triggered Azure Function Locally

1. Navigate to **Visual Studio Code** in your Lab-VM.

1. In your Visual Studio Code, navigate to **Extensions** and install **Azure Functions** and **Azure CLI** extensions.

1. Once the extensions are installed, navigate to **Azure Functions** extension and click on **Create Function Project** under **Workspace (Local)**.

1. While creating the new project, choose the settings based on your preferred language.

   - Select a Language (Python, JavaScript, etc)
   - Select the version
   - Select **HTTP Trigger**
   - Enter the function name
   - Choose **Anonymous** as the authorization level
   - Open in Current/New window
  
1. Your new project will be ready to use locally.

1. In the new VS Code terminal, run the below command to install the **Azure Function Core Tools** extension. Enter **Y** in the terminal to authorize the installation. This might a few minutes to complete the installation process. 

   ```
   winget install Microsoft.Azure.FunctionsCoreTools
   ```

1. Once installed, make sure that you are in the core directory, re-open the VS Code if needed and run the below command to run the function locally.

   ```
   func start
   ```

1. Navigate to the HTTP trigger function via localhost.

## Step 2: Deploy Function to Azure

1. In your Visual Studio Code, navigate to **Azure Functions** extension and **Sign in to Azure**.

1. Click on **Allow** to authorize VS Code.

1. Enter the Azure username and password provided in the **Environment** tab of your lab.

1. Once signed-in, click on **Deploy to Azure** under **Azure Functions** extension.

1. While deploying to Azure, select the following settings:

   - Create a new function app
   - Enter a unique name for your function app
   - Select the location
   - Select the runtime stack
   - Select Secrets as authentication type
  
1. On the VS Code pop-up, click on **Deploy** to deploy the function app to Azure.

1. Once the function app is deployed to Azure, navigate to Azure portal and access the **Default domain** of the function app.

1. Enter the same suffix (example: /api/http-trigger) used while deploying the function app via localhost. 

## Step 3: Configure and Test the Logic App

1. On the Azure portal, search for **Logic Apps** and click on **+ Add**.

1. On the **Create Logic App** page, select the desired hosting option and click on **Select**.

   - Use the same resource group where the newly created function app resides
   - Provide a unique name for your function app
   - Use the default region
   - Click on **Review + Create** and then **Create**

1. Once the Logic App is created successfully, click on **Go to resource**.

1. On the **Logic App** resource, navigate to **Workflows** and **+ Add** a worflow.

1. Your workflow should have three elements:

   - When an HTTP request is received
   - Call an Azure function
   - Response
  
1. In the **When an HTTP request is received** trigger, use the **sample payload** for the parameters.

   ```
   {
     "productId": "75542e38-563f-436f-adeb-f426f1dabb5c"
   }
   ```

1. In the **Call an Azure function** trigger, select **GET** method and leave the other values as default.

1. In the **Response** trigger, configure the following values:

   -  Status Code - **200**
   -  Headers - **product_id > http_trigger**
   -  Body - Enter the same response from the Azure function app API trigger 
  
1. **Save** the workflow and click on **Run**.

1. Once the workflow has run successfully, navigate to the **When an HTTP request is received** trigger and copy the HTTP URL.

1. Paste the HTTP URL in a new browser tab to fetch the logic app's response.
   
