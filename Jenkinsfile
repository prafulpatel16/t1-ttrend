pipeline {
    agent {
        node {
            label "java-slave"
        }
    }

    stages {
        stage('Build') {
            steps {
                echo "------------ Build Started -----------"
                sh 'mvn clean install -Dmaven.test.skip=true'
                echo "------------ Build Completed -----------"
            }
        }

        stage('Sonar Analysis') {
            environment {
                scannerHome = tool 'sonarqube-server' 
            }
            steps {
                echo '<--------------- Sonar Analysis started  --------------->'
                withSonarQubeEnv('sonarqube-server') {
                    sh "${scannerHome}/bin/sonar-scanner"
                }    
                echo '<--------------- Sonar Analysis stopped  --------------->'                
            }
        }
    }
}