def label = "worker-${UUID.randomUUID().toString()}"

node(label){
  stage('SCM') {
       def checkoutVars=checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '8118f0af-166e-456c-8579-d80cc1078bfc', url: 'https://github.com/Karthik-13/example-gradle-app.git']]])
       print(checkoutVars)
   }
  stage('Build'){
    
      sh(script:"./gradlew -q build | xargs echo -n",returnStdout: true)
  }
}

