# API Management


## Scenario #1: Development team authors APIs for internal LOB applications to integrate with.

### API developer process:
#### Overview
An internal dev team for a large enterprise organization is developing a REST API in Azure Functions that pulls people data from an on-premises legacy HR system. Oauth2 is enabled on the Azure Function so clients will need to send a Bearer Token with their requests. There are a number of internal applications about to be migrated to Azure that integrate directly with the HR system's SQL Server from which they pull data. They also have a test SQL server that app teams can test their write operations as to not disturb live data. As part of the migration efforts, the apps will use the Azure Function API instead of a direct SQL connection. The API development team working on this wants to control which applications can have access to this API once they are in Azure and be able to sever access, if needed. They decide to publish their API through Azure API Management so that app owners can use the APIM Developer Portal to request access to published APIs.

#### Steps
1. Developers author the API on their laptops and check them into source control which pushes the code to the Azure Function in their dev environment. This is published in their dev environment as https://people-dev.mycorp.com/v1. The development team uses Postman to test this API directly.

2. When developers are ready to publish their API to production, they push their code which triggers the deployment of the code to their Prod and Test Azure Function environments. These are listening on https://people-test.mycorp.com/v1 and https://people.mycorp.com/v1, respectively. 

3. Once the code is pushed to the production Function, a CI/CD process is triggered and the API is imported or updated in API Management. 

4. Once the API is initially exposed through APIM, the team creates two products: "People API Test" and "People API Prod". They choose to only expose it to gateways in the US because of data residency concerns. All other code pushes will only update the backend APIs, not products. Product modification is required if backend APIs are added or removed from a product. 

### API Consumer Process
#### Overview
As a developer of the corporate intranet being migrated to Azure, a developer is working on the Org Chart feature which pulls data from the HR system. This developer needs to modify their method of connecting to the HR system by using the new API instead of direct SQL. The developer would like to get familiar with the API by using a Postman client before making any code changes.

#### Steps
1. The developer (API consumer) logs into the Developer Portal and can see two products: "People Test API" and "People Prod API" because they were added to the proper AD groups. The developer subscribes to the "People Test API" and because this isn't the production API, the request is auto-approved and the developer receives their subscription key.

2. The developer uses Postman to test the API and ensures that the subscription key is included in the request header. Postman makes two requests: The first request gets a bearer token from the Identity Provider (Azure AD, Okta, etc.). The second request is to the API (https://people-test.mycorp.com/v1/people). Again, the second request must include the bearer token as well as the subscription key. The API gateway will read the incoming request, ensure that it has a valid subscription key, and apply any policies necessary. The gateway will not validate the token in this scenario as the API developers want to control that at the Azure Function. So, as long as a valid subscription key is passed in, the request is sent to the back end.

3. The developer has tested the API and is now ready to begin incorporating it into the intranet code. The developer modifies the code on their local version of the intranet running on their laptop and has their client code call the test API in the "People Test API" product that they already subscribe to. 

4. After they've tested the dev instance of the intranet and they're ready to move to production, they will need to subscribe to the "People API Prod" product to obtain a subscription key. The developers of the API require manual approval of subscription requests to that product. The intranet developer requests to subscribe to the API, it is approved by the API development team, and a subscription key is received.

5. The intranet development team does not want to make the changes to the production intranet to point to the Prod People API without having tested the Prod People API. So, they need to be able to hit the Prod People API from Postman, the dev intranet, as well as the production intranet.
