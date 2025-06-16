# Notify all distributors of the new ice cream line

## Progress Diagram

![Distributor notification progress diagram](images/distributor-notification-progress-diagram.jpg)

## Happy Path

One of these options

* Use Logic Apps, with the Common Data Service & Office 365 Email connectors, and the create HTML Table action or the variables actions  

* Use Logic Apps and Azure Functions together (LA for the Common Data Service and Office 365 Email connectors, and Functions to get the list of products and generate an HTML for it)  

## Coaches Notes

* The CRM Contacts have their email addresses set to two email addresses that you can use to validate the emails were sent. To validate, login with the following accounts OHCoach1@microsoftopenhack.onmicrosoft.com Pass: OpenHackCoach1, User: OHCoach2@microsoftopenhack.onmicrosoft.com, Pass: OpenHackCoach2 at [Office.com](https://outlook.office.com).

* Remember to "Add a new Connection" in Logic Apps when signing in to the Microsoft Dataverse connector connector and enter the credentials as per the challenge.  When entered correctly, the list of options will present.  Select `List Records` then build the logic app around that list with foreach control.

* Use the same connection for both the Microsoft Dataverse connector and the Office 365 Outlook connection

* Use Postman to trigger the logic app to test connections and data outside of the normal workflow.   Don't forget to set the header for content type to `'Content-Type' : 'application/json'`  

* Help them with running the Logic App without the full solution and checking the input/output of each action so they know how to extract the email from the Common Data Service connector response.  Easily create a foreach loop with a logic app connector and select the `Email` property for each contact.

   >NOTE: A solution is available at ~/solutions/codeless/Distributor_Notification/logicapp.json

* Instruct the teams to use the Office 365 Outlook connector to send an email if they need further help [Send Email (v2) action](https://docs.microsoft.com/en-us/connectors/office365connector/#send-an-email-(v2))  

* Attendees should construct the email content using Logic App variables, and insert the variable into the body of the email.  The entire email body could also be a composed variable for simplicity.

* If you get 'Failed to fetch swagger' when using the Azure Functions action in Logic Apps, go back to the function app, into CORS settings, remove all entries and add an entry for `*`.  

* There is a known bug with Logic Apps and the API Management connector, in that the connector is unable to retrieve the list of actions when using the **Consumption** tier of API Management. 

* If you get an error for Microsoft.EventGrid resource provider was not registered for the attendee subscription, make sure to follow the steps to register the EventGrid resource provider from [Register Event Grid as a resource provider](https://docs.microsoft.com/en-us/azure/event-grid/custom-event-quickstart-portal)
