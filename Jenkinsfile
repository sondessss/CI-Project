pipeline {
    agent any
    tools {
        maven "MAVEN"
    }
    stages {
        stage("Maven Build") {
            steps {
                checkout([$class: 'GITSCM' , branches: [[name: '*/master']], extentions: []
                    sh "mvn package -DskipTests=true"
                }
            
        }
        }
        
        }
}
