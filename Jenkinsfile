pipeline {
    agent any
    environment{
        SONARSERVER = 'sonarqube-api'
        SONARSCANNER = 'sonar-scanner'
    }

    stages {

        stage('GIT Checkout') {

            steps {
                git branch: 'main', url: 'https://github.com/Ooladipupo/mrdevops_java_app.git' 
            }
        }
        stage('Unit Test Maven') {

            steps {
                sh 'mvn test'
            }
        }
        stage('Unit Intergration Test') {

            steps {
                sh 'mvn verify -DskipUnitTests'
            }
        }
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('sonarqube-api')
            }
        }
        stage('Quality gate state Sonarqube') {
            environment {
                scannerHome = tool "$(SONARSCANNER)"
            }
            steps {
                withSonarQubeEnv("$(SONARSERVER)") {
                    sh ''' $(scannerHome)/bin/ -Dsonar.host.url=http://44.201.116.224:9000/ -Dsonar.login=squ_c9d95c6b367ff554893cb29ed4a4f99e1b9403f8 -Dsonar.projectName=minikube-sample 
                    -Dsonar.java.binaries=. \
                    -Dsonar.projectkey=minikube-sample''
                }
            }
        }
    }
}
