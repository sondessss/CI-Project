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
       


    
        stage("SonarQube Analysis") {
          agent any  
           steps {
                  withSonarQubeEnv('sonarQube') {
                 sh 'mvn sonar:sonar'
                  }
           }
         }

    }
}
