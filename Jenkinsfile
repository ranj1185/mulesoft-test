pipeline {
   agent any
   stages { 
/**
*Initialize pipeline variables:
*prodAPIList - Array that will contain APIs deployed in Production
*appsDeletedFromDEV - Array that will contain APIs deleted from DEV
*appsDeletedFromSIT - Array that will contain APIs deleted from SIT
*appsToIgnore - Configure the names of APIs that shouldn't be part of this logic. Used to specify those critical APIs that should never be deleted.
*devEnvironmentID - ARM Environment ID for DEV
*sitEnvironmentID - ARM Environment ID for SIT
*prodEnvironmentID - ARM Environment ID for PROD
*/
stage('Initialize') {
            steps {
                script {
                    prodAPIList = [] 
                    appsDeletedFromDEV = [] 
                    appsDeletedFromSIT = [] 
                    appsToIgnore = ["XXXX"] 
                    devEnvironmentID = "XXXX" 
                    sitEnvironmentID = "XXXX" 
                    prodEnvironmentID = "XXXX" 
                }
            }
        }
/**
*Invoke the Login API to generate the access_token.
*Note: It is recommended to inject the platform credentials through Jenkins Credentials Plugin
*/
        stage('Login to ARM') {
            steps {
                script {
                    def loginContents = httpRequest consoleLogResponseBody: true, contentType: 'APPLICATION_JSON', httpMode: 'POST', ignoreSslErrors: true, requestBody: '{"username":"XXXX","password":"XXXX"}', responseHandle: 'NONE', timeout: 30000, url: 'https://anypoint.mulesoft.com/accounts/login', validResponseCodes: '200'
                    authToken = 'Bearer ' + new groovy.json.JsonSlurper().parseText(loginContents.getContent()).access_token;
                }
            }
        }
   	}
}
