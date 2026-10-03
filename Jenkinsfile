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

    }
}