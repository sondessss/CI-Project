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
                  sh 'mvn sonar:sonar -Dsonar.projectKey=myProject -Dsonar.host.url=http://172.20.10.7:9000 -Dsonar.login=94a1dd02a29ad288b0966f5dbb388eec962433fa'
                  echo 'sonar static analysis done'
           }
         }

    }
}
