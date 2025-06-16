# System telemetry and API Management

## Progress Diagram

![System telemetry and API Management progress diagram](images/system-telemetry-and-api-management-progress-diagram.jpg)

## Happy Path

### For Telemetry

Enable App Insights, then run the create the query provided in the solutions directory in App Insights Analytics:

### For API Management

* Try to coach towards the path of API Management. Features that will want to harness include
    * Reverse Proxy
    * Product Groups
    * Rate Limit policies

## Coaches Notes

* Explain to your team differences between API Management versus Proxies.
* APIM will not accept the email address with the "onmicrosoft.com" domain for the admin email. The team will need to use a valid email address in this field.
* Make them aware of how long a non Consumption based sku takes to deploy and if they want to go that way make them create the account ASAP. Otherwise the consumption sku is much faster to deploy and will contain the features required to accomplish the challenge.
