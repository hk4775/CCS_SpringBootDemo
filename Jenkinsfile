node {
   stage('init') {
      checkout scm
   }
   stage('build') {
      sh '''
         mvn clean package
         cd target
         cp ../src/main/resources/web.config web.config
         cp ccs-rest-service-0.1.0.jar app.jar 
         jar -cf ccs.zip app.jar web.config
      '''
   }
   stage('deploy') {
      azureWebAppPublish azureCredentialsId: env.AZURE_CRED_ID,
      resourceGroup: env.RES_GROUP, appName: env.WEB_APP, filePath: "**/ccs.zip"
      println env.WEB_APP
      println env.RES_GROUP
   }
}
