pipeline {
    agent any 
    stages {
        stage('Build') {
            steps {
                echo 'Hello world!' 
            }
        }
        stage('SonarQube analysis') {
            steps {
                script {
                    scannerHome = tool 'sonarqubeScannerInstallation'// must match the name of an actual scanner installation directory on your Jenkins build agent
                }
                withSonarQubeEnv('sonarqubeInstallation') {// If you have configured more than one global server connection, you can specify its name as configured in Jenkins
                  sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }
        stage('dependencyTrackPublisher') {
            steps {
                withCredentials([string(credentialsId: '506ed685-4e2b-4d31-a44f-8ba8e67b6341')]) {
                    dependencyTrackPublisher artifact: 'target/bom.xml', projectName: 'Test_Con4', projectVersion: '1.2', synchronous: true
                }
            }
        }
    }
}
