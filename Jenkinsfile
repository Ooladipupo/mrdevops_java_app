pipeline {
    agent any

    stages {

        stage('GIT Checkout') {

            steps {
                git branch: 'main', url: 'https://github.com/Ooladipupo/mrdevops_java_app.git' 
            }
        }
        // stage('Unit Test Maven') {

        //     steps {
        //         sh 'mvn test'
        //     }
        // }
        // stage('Unit Intergration Test') {

        //     steps {
        //         sh 'mvn verify -DskipUnitTests'
        //     }
        // }
        stage('static code analysis Sonarqube') {

            steps {
                withSonarQubeEnv('sonarqube-api') {
                sh ''' mvn sonar:sonar -Dsonar.host.url=http://44.201.116.224:9000/ -Dsonar.login=squ_c9d95c6b367ff554893cb29ed4a4f99e1b9403f8'''
            }
        }
        // stage('quality gate') {
            
            steps {
               withSonarQubeEnv('sonarqube-api') {
                waitForQualityGate abortPipeline: true }
            }
        }
    }
}
}
