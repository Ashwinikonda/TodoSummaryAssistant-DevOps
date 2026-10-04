pipeline {
    agent any

    stages {

        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Maven Test') {
            steps {
                dir('Backend/todo-summary-assistant') {
                    withEnv([
                        'COHERE_API_KEY=dummy',
                        'SLACK_WEBHOOK_URL=dummy',
                        'SPRING_DATASOURCE_URL=jdbc:mysql://todo-mysql:3306/todo_db',
                        'SPRING_DATASOURCE_USERNAME=root',
                        'SPRING_DATASOURCE_PASSWORD=tiger'
                    ]) {
                        sh './mvnw test'
                    }
                }
            }
        }

        stage('Docker Build') {
            steps {
                sh 'docker build -t todo-backend:ci Backend/todo-summary-assistant'
                sh 'docker build -t todo-frontend:ci Frontend/todo'
            }
        }

        stage('Tag Images') {
            steps {
                script {
                    def commit = sh(
                        script: 'git rev-parse --short HEAD',
                        returnStdout: true
                    ).trim()

                    env.IMAGE_TAG = commit

                    sh "docker tag todo-backend:ci ashwiniskonda/todo-summary-backend:${commit}"
                    sh "docker tag todo-frontend:ci ashwiniskonda/todo-summary-frontend:${commit}"
                }
            }
        }

        stage('Docker Push') {
            steps {
                withCredentials([
                    usernamePassword(
                        credentialsId: 'dockerhub-creds',
                        usernameVariable: 'DOCKERHUB_USERNAME',
                        passwordVariable: 'DOCKERHUB_TOKEN'
                    )
                ]) {
                    sh '''
                        echo "$DOCKERHUB_TOKEN" | docker login -u "$DOCKERHUB_USERNAME" --password-stdin

                        docker push ashwiniskonda/todo-summary-backend:${IMAGE_TAG}
                        docker push ashwiniskonda/todo-summary-frontend:${IMAGE_TAG}

                        docker logout
                    '''
                }
            }
        }

    }
}