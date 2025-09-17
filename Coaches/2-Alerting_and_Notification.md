# Alerting and notification

## Progress Diagram

![Alerting and notification progress diagram](../images/alerting-and-notification-progress-diagram.jpg)

## Happy Path

* Edit the existing CreateRating function and put userNotes through either:
    * Text Analytics Cognitive Services API calls
    * [TextBlob](https://textblob.readthedocs.io/en/dev/index.html#) library using Python functions
* Create Custom Telemetry to write to the same App Insights instance as the function whenever there’s a bad review
* Use the Log Alerts feature for Application Insights to generate an alert and email when the threshold is reached

[How To - Sentiment Analysis](https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis?tabs=version-3)  

## Challenge 1: Add Sentiment Analysis + Custom Telemetry

### Step 1: Enable Text Analytics (Azure AI Language)

1. Navigate to Azure portal and create a **Language** service.

1. On the **Select additional features** tab, click on **Continue to create your resource**. Note that, ***Sentiment Analysis*** is one of the default features.

1. On the **Create Language** blade, configure the following settings and click on **Review + Create** and then **Create**.

   - Use the resource group **serverless-openhack**
   - Select your desired region
   - Provide a unique name for your resource
   - Select **Standard - S** as pricing tier
   - Acknowledge the **Responsible Use of AI Documentation for Language** checkbox
  
1. Once the deployment is complete, go to your newly created Language resource, navigate to **Keys and Endpoint** setting from the left navigation pane and note down the **Key** and **Endpoint** in a notepad.

## Step 2: Update `CreateRating` Function

1. 
