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
                sh 'mvn clean package sonar:sonar'
            }
        }
    }
}
