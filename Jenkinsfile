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
   
        stage("compile Project"){
            steps {
                 sh 'mvn compile -X -e'
                  echo 'compile stage done'
            }
        }
        stage("unit tests"){
            steps {
                 sh 'mvn test'
                  echo 'unit tests stage done'
            }
        }
       
        stage("SonarQube Analysis") {
           steps {
                  withSonarQubeEnv('sonarQube') {
                 sh 'mvn sonar:sonar'
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

    }
}
