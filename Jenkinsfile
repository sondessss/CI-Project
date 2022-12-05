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

        stage("unit tests"){
            steps {
                 sh 'mvn test'
                  echo 'unit tests stage done'
            }
        }
        stage("compile Project"){
            steps {
                 sh 'mvn compile -X -e'
                  echo 'compile stage done'
            }
        }
        stage("mvn Pckage") {
            steps {
                script {
                    sh "mvn package -DskipTests=true"
                }
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
