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
         stage("mvn Pckage") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }
        
        
          stage("Upload Jar  To Nexus") {
            steps {  
               nexusArtifactUploader artifacts: [ 
                 [ 
                    artifactId: 'tpAchatProject',  
                      classifier: '',  
                      file: 'target/tpAchatProject-1.0.jar',   
                      type: 'jar'
                     ]
                 ],
                   
            credentialsId: 'nexus', 
            groupId: 'com.esprit.examen', 
            nexusUrl: '172.20.10.8:8081', 
            nexusVersion: 'nexus3', 
            protocol: 'http', 
            repository: 'maven-releases',  
            version: '1.0' 


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
             
          stage("DockerHub login ") {
              steps{
                  sh 'echo $DOCKERHUB_CREDENTIALS_PSW | docker login -u espritadmin -p initiationcloud'
            }
          }

          stage('Docker-compose file') {

              steps {
                   sh 'docker-compose up -d';
                    sh 'sleep 300'
              
             }  
        }

}
}
