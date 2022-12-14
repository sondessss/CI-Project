pipeline {
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
          stage("Nexus Deploy") {
            steps {
                script {
                    sh "nexusArtifactUploader artifacts: [[artifactId: 'tpAchatProject', classifier: '', file: 'target/tpAchatProject-1.0.jar', type: 'jar']],
                     credentialsId: '',
                     groupId: 'com.esprit.examen',
                     nexusUrl: '172.20.10.7/8081',
                     nexusVersion: 'nexus2',
                     protocol: 'http',
                     repository: 'http://172.20.10.7:8081/repository/java-Re',
                     version: '1.0'"
                }
            }

          }
    }
}
