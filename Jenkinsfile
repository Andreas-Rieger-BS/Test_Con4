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
                 dependencyTrackPublisher artifact:'bom.xml', projectName: 'Test_Con4', projectVersion: '1.2', projectId: 'a65ea72b-5b77-40c5-8b19-fb83525f40eb', synchronous: true
            }
        }
    }
}
