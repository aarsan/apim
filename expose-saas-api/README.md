# API Management

## Line of Business app teams desire to pull in ServiceNow data. 

### Overview
Multiple application teams are requesting access to the ServiceNow API to integrate their applications with. Because ServiceNow is a SaaS product, all applications that require access to it will need internet access. The team that manages the ServiceNow subscription thought they would have better control over who is using the API if they published it through Azure API Management so that consumers of the API can simply go to the developer portal and request access. The applications consumping this API also do not need internet access as the published endpoint is on the internal network.