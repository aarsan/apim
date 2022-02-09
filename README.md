
# Demo Environment or Workflow Diagrams for API Management Use-cases in Financial Services

This API Management environment shows how a real-world insurance company can transform their business by creating an API economy that bolsters innovation and allows Big Insurance to enter new markets.


## Workflow Demos

- Autoscaling based on load
- Throttling Demo
  - Showcase throttling at the Backend and API Gateway
- Product Management Demo

### Products

### Back-end APIs

- Claims Processing App
  - Mock Flask API running in App Service
  - Client submits frequent claims (tunable)

- Pet Insurance Quote API
  - Mock Flask API running in App Service
  - Client submits quote request

### Front-End UIs

- Claims Submission App
  - Submit single claim
  - Submit multiple claims
  - Monitor Claim Statuses
  - Postman

### Roles

1. Back-end API owner
2. Developer consuming APIs via APIM.
3. Platform Operators
4. Cost Management

Digital Transformation for business growth, not for cool tech. 
- customers to innovate by creating an ecosystem of APIs available to the organization

In this example scenario, we have a fictitious insurance company, Acme Insurance Company, that provides auto and pet insurance. They have a reseller program which allows anyone to sell their insurance for them and make a commission. To the resellers, Acme provides a website where they can log into to purchase insurance and manage their claims. This works well for smaller resellers but many of them already have a system in place and having to disrupt their flow and use another system to make claims will not work for them. Acme provides an API that can be used for integrating with existing claims processing systems.

## Use Case

Acme Insurance signs up new resellers, sells policies, and  processes claims everyday. The resellers are located all over the United States. Both the website as well as the API need to be up and running 24/7/365. 


- [Development team authors APIs for internal LOB applications to integrate with.](https://github.com/aarsan/apim/tree/master/onprem-legacy-api)

- [Internal LOB apps desire access to ServiceNow API.](https://github.com/aarsan/apim/tree/master/expose-saas-api)
