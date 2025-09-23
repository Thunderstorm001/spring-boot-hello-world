pipeline {
    agent any

    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
        APP_PORT = '9090'
        JAR_NAME = 'spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Thunderstorm001/spring-boot-hello-world.git'
                echo "Done Checkout"
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests' // Skip tests here if you want faster build
                echo "Done Build"
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test' // Run tests separately
                echo "Done Test"
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                # Kill existing app on the port
                fuser -k ${APP_PORT}/tcp || true

                # Run Spring Boot app in background
                nohup java -jar target/${JAR_NAME} --server.port=${APP_PORT} > app.log 2>&1 &
                disown

                echo "Spring Boot app started on port ${APP_PORT}"
                '''
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
    }
}
