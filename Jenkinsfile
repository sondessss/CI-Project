pipeline {
    environment{
    registry="espritadmin/my1st-deploy"
    registryCredential = "espritadmin-dockerhub"
        dockerImage = "my1st-image"
    }
    agent any
    stages {
        stage("Cloning Project"){
            steps {
                git branch: 'master',
                url: 'https://github.com/sondessss/CI-Project.git'
                echo 'checkout stage'
            }
        }
               
        stage ('MVN clean') {
      steps {
        sh 'mvn clean -e'
        echo 'Build stage done'
      }
    }
   
        stage('build') {
            steps{
               script {
               dockerImage=docker.build registry + ":$BUILD_NUMBER"
               }
             }
            }
         stage("docker push") {
              steps{
                 script {
                 docker.withRegistry( '', registryCredential ) {
                 dockerImage.push()
              }
             }
           }
}
}
}
