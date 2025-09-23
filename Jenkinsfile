pipeline{
  agent any
  environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        PATH = "${env.JAVA_HOME}/bin:${env.PATH}"
    }
  stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/Thunderstorm001/spring-boot-hello-world.git'
            }
        }

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

        stage('Run App') {
            steps {
                sh 'nohup java -jar target/spring-boot-2-hello-world-1.0.2-SNAPSHOT.jar --server.port=9090 > app.log 2>&1 &'
            }
        }
    }
}
