pipeline {
    environment{
    registry="espritadmin/my1st-deploy"
    registryCredential="dockerHub"
        DockerImage="mybackImage"
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
         stage("mvn Pckage") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }
   
        stage('build') {
            steps{
               script {
               dockerImage=docker.build registry + ":$BUILD_NUMBER"
               }
             }
            }
         stage('push to dockerhub') {
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
