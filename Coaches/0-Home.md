# Serverless OpenHack

## Scenarios

The challenges in this Serverless OpenHack are based on real world and validated scenarios from customers:

* **Application Backend / API Hosting** - A very common scenario, utilizing Azure Functions and Logic Apps to implement a full API for a solution. Sometimes the API itself is the main solution that the customer sells; it can be combined with Azure API Management.

* **Business and Systems Integration with Workflow** - A recurring scenario with customers is to create a workflow between multiple systems (systems integration); some are business workflow often with human interaction (business workflow).

* **User or Telemetry data processing** - Using Azure Functions to process, split, or forward external user and telemetry data coming in via Event Hubs, IoT Hub, or other; and running a workflow using Logic Apps for specific alerts. Good fit for solutions with under 100,000 messages per second with no actor model requirements.

There are many other scenarios for serverless of course; we are only covering these that have been validated by CSE with multiple customers. This should give the audience a good understanding of serverless on Azure and how it works with the rest of the Azure services.

## Target Audience

The event targets all developers but has an emphasis on developers building business and enterprise solutions. These challenges are very compelling to ISVs as well as they go well with the microservices architecture with a consumption-based plan.

Attendees do not need previous knowledge of Azure or Azure Serverless offerings. Its preferred to have basic knowledge of C# or Node.js but is not a requirement.

## Goals

On top of general OpenHack goals to improve Azure services, improve documentation, and evangelize these technologies, there are other goals we are focused on:

* Emphasize the time to market and ease of getting applications built using serverless

* How serverless can bring a varied of PaaS services together with ease of integration

* Expand integration for enterprise scenarios to bring business applications together

* Help upskill attendees on how serverless can solve real world problems when communicating with various modules

## Challenges Summary

| Title | Challenge Overview | Possible Technologies |
|-------|--------------------|-----------------------|
| 1 - Development environment configuration | Getting the teams development environments configured for the challenges to come |
| 2 - Create your first serverless function & workflow | Create & debug an Azure Function locally,  deploy the function to Azure, test with Postman or other. Create the first Logic App | Functions, Logic Apps
| 3 - Finishing the Ice Cream Ratings API, and Continuous Integration and Deployment | Create the Ratings function app to finish the company's API while implementing a CI/CD pipeline for the team to work with | Functions, Cosmos DB, Azure DevOps, Jenkins, Kudu, other CI/CD solutions
| 4 - System telemetry and API Management | Enable telemetry for the API, show usage and average call durations for the past hour. Consolidate all function apps behind one base URL, implement rate limiting policies while exposing APIs as different suites of products | Application Insights, AI Analytics, API Management
| 5 - Distributor notification | Iterate through distributors and send them emails with the details of the new ice cream line | Logic Apps, Azure Functions
| 6 - Process distributor order batch files | Wait for a batch of files to arrive and process them once all files arrive for a batch | Storage, Event Grid, Logic Apps, Durable Functions, Functions
| 7 - Process POS sales events | Process POS sale events as they arrive in batches. Handle a large number of events and monitor auto scale. | Event Hubs, Functions, Cosmos DB
| 8 - Pub/Sub and network integration | Store different receipt URL data for further analysis within a private virtual network. | Service Bus, Premium Functions, Storage Accounts
| 9 - Alerting and notifications | Add Sentiment Analysis to user comments from ratings and generate email alerts when a number of bad reviews from customers arrives over the last 5 minutes | Logic Apps, Functions
| 10 - Putting it All Together | Combining the data from all sources to create insights for management | Cosmos DB, Stream Analytics, Power BI

## What does a coach do

### Hacker Teams

* Facilitate Collaboration​
* Set expectations​
* Ask leading questions, offer resources instead of answers​
* Encourage creativity​
* Problem solve: technical and interpersonal

### Manage Sentiment

* Content will be challenging and **frustrating** at times​
* Let them be challenged but not blocked​
* Check in frequently and raise any issues or what is working well

### Coach Team

* Share challenges, solutions​
* Leverage **Teams** channel​
* Collect **daily feedback** for end-of-day coaches sync​
* **Take breaks** and check in with the coaches around you

## End of day sync

For the internal coaches sync at the end of each day, there are three questions you should ask each of your teams:

* What did you accomplish today?
* What was the biggest challenge today?
* Is there anything we can do better tomorrow?

## Some things to keep in mind

* No step-by-step instructions or “right” answer​
* Not all pain points are removed​
* Everyone should be learning and having fun. That includes YOU!​
* Keep Challenge Content and reference solutions private​
* Teams probably won’t complete all challenges. Even though we have a leaderboard, it’s important that they learn and not cut corners, it’s ok for them to stay in the early challenges, and the objective is NOT to finish all challenges

## Code of conduct

Microsoft’s mission is to empower every person and every business on the planet to achieve more. This includes at OpenHack where we seek to create a respectful, friendly, and inclusive experience for all participants.​

As such, we do not tolerate harassing or disrespectful behavior, messages, images, or interactions by any event participant, in any form, at any aspect of the program including business and social activities, regardless of location.​

We do not tolerate any behavior that is degrading to any gender, race, sexual orientation or disability, or any behavior that would violate Microsoft’s Anti-Harassment and Anti-Discrimination Policy, Equal Employment Opportunity Policy, or Standards of Business Conduct. In short, the entire experience at the venue must meet our culture standards.​

We encourage everyone to assist in creating a welcoming and safe environment. Please report any concerns, harassing behavior, or suspicious or disruptive activity to venue staff, the event host or owner, or the nearest security guard or event staff. ​

Microsoft reserves the right to refuse admittance to, or remove any person from OpenHack at any time in its sole discretion.

We ask you to take a leadership role in helping to ensure this event is a success for your peers and our customers. How you can help:​

* **Prioritize the satisfaction of our customers and partners above all else**. Extend your kindness and courtesy to all other attendees and help event staff as needed.​
* Ensure all attendees are **respectful and supportive of other attendees**. If someone is being excluded, ignored or interrupted, please take time to politely direct the group to be respectful. E.g. “I don’t think they have finished their thought”​
* **Immediately report any incidents** to the Event Crew that are harassing or disrespectful regardless of gender, race, sexual orientation or disability.​
* Remember that while there will be a number of Microsoft employees hacking through the challenges. The majority of attendees are external. **Please refrain from discussing any Microsoft confidential information at the event or ancillary activities. ​**
* Do not use open forums with Microsoft SMEs (E.g. lunchtime presentations) to ask internal or “Hardball” questions. Microsoft attendees should instead find private time to ask these questions or provide feedback.
