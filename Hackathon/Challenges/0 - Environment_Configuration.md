# Development Environment Configuration


* Your preferred IDE (integrated development environments), like
Visual Studio Code or Visual Studio:
    * If using Visual Studio for Windows, make sure you have the
  [latest Visual Studio 2019](https://visualstudio.microsoft.com/)
  with the `Azure development workload` selected,
  and the most recent version of the
  [Azure Functions and Web Jobs Tools extension](https://docs.microsoft.com/azure/azure-functions/functions-develop-vs#check-your-tools-version)

    * If using Visual Studio Code in Windows, OSX, or Linux make sure you have the latest Visual Studio Code version for your OS, and  

        * [VSCode Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)

        * [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local)

## Language specific prerequisites

Depending on the language your team uses, there are additional prerequisites that your machine will need to have. Please review these language specific prerequisites to ensure your machine is ready for the open hack.

### C# / .NET

* Either [Visual Studio 22](https://visualstudio.microsoft.com/)

or

* [Visual Studio Code](https://code.visualstudio.com/) on one of the [supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).  

    * Use of the Visual Studio Code [C# Extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) is recommended.

    * [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local) 



### Java/Maven

* [Java Developer Kit](https://aka.ms/azure-jdks) 
* [Apache Maven](https://maven.apache.org/) 
* [Azure CLI](https://docs.microsoft.com/cli/azure)
* [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local#) 

> Refer to [Azure Functions Java Developer guide](https://docs.microsoft.com/azure/azure-functions/functions-reference-java) for latest version support information

### JavaScript

* [Visual Studio Code](https://code.visualstudio.com/) on one of the [supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms)
* [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local)
* [Node.js](https://nodejs.org/) 

> Refer to [Azure Function Supported Languages](https://docs.microsoft.com/azure/azure-functions/functions-reference-java) for further Node supported version information

### Python  
 

#### Use a VM instead of multiple versions  

It is recommended you do not do a side-by-side installation of a new python version for this challenge.  To be clean and avoid potential issues, consider using a low-cost VM running on linux at Azure and install the latest python tools there.  

#### Use VSCode with the Azure Functions Extension  

It is very easy to work with VSCode with python functions at Azure.  Although you may be new to VSCode, it is recommended due to the high availability of extensions that can easily run (locally) and publish Azure functions to your integrated Azure subscription.  

* [Python](https://www.python.org/downloads/)  

    * Using VSCode with Azure Functions extension makes it easy to select the compiler. language, and project and integrate directly to your function app at Azure, including deployment.  

    * VS Code users on Windows, in the past, python interpreter selection can be troublesome. Review [Python in VS Code environments](https://code.visualstudio.com/docs/languages/python#_environments) for assistance with this if you run into issues.  

* [VSCode](https://code.visualstudio.com/download)  

* [VSCode Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)  

* [Azure Functions Core Tools](https://docs.microsoft.com/azure/azure-functions/functions-run-local#v3) version 3x.  You need this to run/test locally.  

* [Azure CLI](https://docs.microsoft.com/cli/azure)

* Recommended for Mac OSX and Linux users to install  [Azurite](https://www.nuget.org/packages/Azurite/)  

* [VSCode Azure Storage extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage)  
