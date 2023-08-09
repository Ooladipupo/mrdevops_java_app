pipeline {
    agent any

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
        stage('static code analysis Sonarqube') {

            steps {
                sh 'mvn clean package'
                sh ''' mvn sonar:sonar -Dsonar.host.url=http://44.202.37.0:9000/ -Dsonar.login=squ_c9d95c6b367ff554893cb29ed4a4f99e1b9403f8'''
            }
        }
            stage('static code analysis Sonarqube') {

            steps {
                script{
                    def sonarQubeCredentials = 'sonarqube-api'
                    sh 'waitForQualityGate abortPipeline: false, credentialsId: 'sonarQubeCredentials'
                }
            }
        }
    }
}
