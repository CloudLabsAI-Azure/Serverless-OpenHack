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
