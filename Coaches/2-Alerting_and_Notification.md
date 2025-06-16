# Alerting and notification

## Progress Diagram

![Alerting and notification progress diagram](/images/alerting-and-notification-progress-diagram.jpg)

## Happy Path

* Edit the existing CreateRating function and put userNotes through either:
    * Text Analytics Cognitive Services API calls
    * [TextBlob](https://textblob.readthedocs.io/en/dev/index.html#) library using Python functions
* Create Custom Telemetry to write to the same App Insights instance as the function whenever there’s a bad review
* Use the Log Alerts feature for Application Insights to generate an alert and email when the threshold is reached

[How To - Sentiment Analysis](https://docs.microsoft.com/en-us/azure/cognitive-services/text-analytics/how-tos/text-analytics-how-to-sentiment-analysis?tabs=version-3)  
