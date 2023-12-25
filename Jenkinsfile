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


        #stage("Quality Gate"){
        #    steps {
        #       script {
        #          timeout(time: 1, unit: 'HOURS') { // Just in case something goes wrong, pipeline will be killed after a timeout
        #               def qg = waitForQualityGate() // Reuse taskId previously collected by withSonarQubeEnv
        #               if (qg.status != 'OK') {
        #                   error "Pipeline aborted due to quality gate failure: ${qg.status}"
        #               }
        #           }
        #       }
        #   }
        #}

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