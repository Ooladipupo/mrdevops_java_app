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
    }
}
