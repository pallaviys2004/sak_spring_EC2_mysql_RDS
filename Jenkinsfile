pipeline {
    agent any

    tools {
        maven 'maven'
    }

    stages {

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Run Spring Boot Application') {
            steps {
                sh '''
                    echo "Stopping existing application..."
                    pkill -f spring_app_sak-0.0.1-SNAPSHOT.jar || true

                    echo "Starting application..."
                    nohup java -jar target/spring_app_sak-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
                '''
            }
        }
    }

    post {
        success {
            echo 'Pipeline Success'
        }
        failure {
            echo 'Pipeline Failed'
        }
    }
}