node {
  stage('init') {
    checkout scm
  }
  
  stage('deploy') {
    
    // login Azure
    withCredentials([azureServicePrincipal('customerzeroonboard')]) {
      sh '''
        az login --service-principal -u $AZURE_CLIENT_ID -p $AZURE_CLIENT_SECRET -t $AZURE_TENANT_ID
        az account set -s $AZURE_SUBSCRIPTION_ID
      '''
    }
    
    // deploy/update app
    sh "az webapp up --resource-group $RES_GROUP --plan $WEB_APP_PLAN --name $WEB_APP --sku FREE --subscription $SUBSCRIPTION --location $LOCATION"
    
    // logout Azure
    sh 'az logout'
  }
}
