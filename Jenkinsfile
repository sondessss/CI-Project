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

    
        stage("SonarQube Analysis") {
          agent any  
           steps {
                  sh 'mvn sonar:sonar'
                  echo 'sonar static analysis done'
           }
         }

    }
}
