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
                script {
                    echo "------------ Sonar Analysis Started -----------"
                    withSonarQubeEnv('sonarqube-server') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=prafulpatel16_t1-ttrend -Dsonar.organization=prafulpatel16"
                    }
                    echo "------------ Sonar Analysis Completed -----------"
                }
            }   
        }
    }
}