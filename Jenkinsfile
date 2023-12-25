pipeline {
    agent {
        node {
            label 'maven'
        }
    }

    environment {
        PATH = "/opt/apache-maven-3.9.6/bin:$PATH"
    }

    stages {
        stage("mvn build stage") {
            steps {
                echo "----------- build started ----------"
                sh 'mvn clean deploy'
                echo "----------- build completed ----------"
            }
        }

        stage('SonarQube analysis') {
        environment {
            scannerHome = tool 'Nag-SonarQube-Scanner'
        }
            steps {
                script {
                    withSonarQubeEnv('Nag-SonarQube-servers') {
                        sh "${scannerHome}/bin/sonar-scanner"
                    }
                }
            }
        }
    }
}