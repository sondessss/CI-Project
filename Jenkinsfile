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
          agent any  
           steps {
                  sh ''mvn clean verify sonar:sonar -Dsonar.projectKey=AchatProject -Dsonar.host.url=http://http://172.20.10.7:9000 -Dsonar.login=admin1'
                  echo 'sonar static analysis done'
           }
         }
         
          stage("mvn Pckage") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
            }
        }
        stage("Nexus Deploy") {
            steps {
                script {
                    sh "mvn clean package deploy:deploy -DgroupId=com.esprit.examen -DartifactId=tpAchatProject -Dversion=1.0 -DgeneratePom=true -Dpackaging=jar -DrepositoryId=deploymentRepo -Durl=http://http://172.20.10.7:8081/repository/maven-releases/ -Dfile=target/tpAchatProject-1.0.jar"
                }
            }
        }
    }
}
