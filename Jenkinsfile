def label = "worker-${UUID.randomUUID().toString()}"

podTemplate(label: label, containers: [
  containerTemplate(name: 'jenkins-slave', image: 'jenkinsci/jnlp-slave', command: 'cat', ttyEnabled: true),
  containerTemplate(name: 'gradle-slave', image: 'openjdk:8-jdk-alpine', command: 'cat', ttyEnabled: true)
])
{
node(label){
  stage('SCM') {
    vmnBuild("SCM") {
      container('gradle-slave'){
       checkout([$class: 'GitSCM', branches: [[name: '*/master']], doGenerateSubmoduleConfigurations: false, extensions: [], submoduleCfg: [], userRemoteConfigs: [[credentialsId: '8118f0af-166e-456c-8579-d80cc1078bfc', url: 'https://github.com/Karthik-13/example-gradle-app.git']]])
      }
    }
   }
  stage('Build'){
     vmnBuild("Build") {
    container("gradle-slave") {
            sh(script:"./gradlew -q build | xargs echo -n",returnStdout: true)
        }
    }
  }
}
}

