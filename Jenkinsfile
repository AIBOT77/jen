pipeline {
    agent any

    tools {
        maven 'Maven 3.9.6'
        jdk 'Java 17'
    }

    environment {
        SONARQUBE_SCANNER_PARAMS = '-Dsonar.projectKey=your-project -Dsonar.host.url=http://sonarqube:9000 -Dsonar.login=${SONAR_AUTH_TOKEN}'
    }

    stages {
        stage('Checkout') {
            steps {
                git credentialsId: 'github-token', url: 'https://github.com/AIBOT77/jen.git', branch: 'main'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('SonarQube Analysis') {
            steps {
                withSonarQubeEnv('LocalSonar') {
                    sh 'mvn sonar:sonar'
                }
            }
        }
    }
}
