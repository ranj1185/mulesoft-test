//exchangeDetail & token from the previous steps are passed as arguments
 
def createAPIInstance(token, exchangeDetail)
 def requestTemplate = '{ "endpoint": { "deploymentType": null, "isCloudHub": null, "muleVersion4OrAbove": null, "proxyUri": null, "referencesUserDomain": null, "responseTimeout": null, "type": null, "uri": null }, "instanceLabel": null, "spec": { "assetId": null, "groupId": null, "version": null } }'
def request = new JsonSlurper().parseText(requestTemplate);
request.endpoint.deploymentType = 'CH'
request.endpoint.uri = ''
request.endpoint.type = 'rest-api'
request.spec.assetId =  exchangeDetails.assetId
request.spec.groupId =  exchangeDetails.groupId
request.spec.version = exchangeDetails.version
 
def message = JsonOutput.toJson(request)
log(INFO, "createAPIInstance request message=" + message);
def urlString = "https://anypoint.mulesoft.com/apimanager/api/v1/organizations/"+props.orgId+"/environments/"+props.envId + "/apis"
def headers = ["Content-Type": "application/json", "Authorization": "Bearer "+ token]
def connection = doRESTHTTPCall(urlString, "POST", message, headers)
def response = "${connection.content}"
if (connection.responseCode = ~'2..') {
 log(INFO, "the API instance is created successfully! statusCode=" + connection.responseCode)
} else {
 throw new Exception("Failed to create API Instance! statusCode=${connection.responseCode} responseMessage=${response}")
}
def apiInstance = new JsonSlurper().parseText(response)
log(DEBUG, "END createAPIInstance " + apiInstance)
return apiInstance;
}
