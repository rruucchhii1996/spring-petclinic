pipeline {
    agent any

    stages {

                stage('Checkout') {
            steps {
                checkout([
                    $class: 'GitSCM',
                    branches: [[name: '*/cicd']],
                    extensions: [[$class: 'CleanBeforeCheckout']],
                    userRemoteConfigs: [[
                        url: 'https://github.com/rruucchhii1996/spring-petclinic.git',
                        credentialsId: 'rruucchhii1996'
                    ]]
                ])
            }
        }

        stage('Clone') {
            steps {
                git 'https://github.com/rruucchhii1996/spring-petclinic.git'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t petclinic-app .'
            }
        }

        stage('Run Container') {
            steps {
                sh '''
                docker stop petclinic || true
                docker rm petclinic || true
                docker run -d -p 8085:8080 --name petclinic petclinic-app
                '''
            }
        }
    }
}
