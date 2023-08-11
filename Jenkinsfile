pipeline {
    agent any
    environment{
        DOCKERHUB = 'ola22/testing'
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
        stage('static code analysis Sonarqube') {

            steps {
                withSonarQubeEnv('sonarqube-api') {
                sh ''' mvn sonar:sonar -Dsonar.host.url=http://44.201.116.224:9000/ -Dsonar.login=squ_c9d95c6b367ff554893cb29ed4a4f99e1b9403f8'''
            }
        }}
        stage('quality gate') {
            
            steps {
               withSonarQubeEnv('sonarqube-api') {
                waitForQualityGate abortPipeline: false }
            }
        }
        stage('maven Build') {

            steps {
                sh 'mvn clean install'
            }
        }
        stage('Docker Image Build') {

            steps {
               sh """ docker build -t $DOCKERHUB .
               docker tag $DOCKERHUB $DOCKERHUB:V1.2
               """
            }
        }
        // stage('Trivy Image Scan') {

        //     steps {
        //         sh """
        //         trivy image $DOCKERHUB:V1.2 > scan.txt
        //         cat scan.txt
        //         """
        //     }
        // }
        stage('Docker Image Push to DockerHub') {

            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'DockerHub', 
                    passwordVariable: 'PASS', 
                    usernameVariable: 'USER'
                )])
                script{ docker login -u "$USER" -p "$PASS"
                            sh "docker push $DOCKERHUB:V1.2"}
            }
        }
    }
}


