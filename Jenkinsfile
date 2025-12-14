pipeline {
    agent any

    tools {
        maven 'M3'
    }

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        tage('Build Contracts') {
            steps {
                sh 'cd events-contract && mvn clean install -DskipTests'
                sh 'cd books-api-contract && mvn clean install -DskipTests'
            }
        }

        stage('Build Services') {
            steps {
                sh 'cd demo-rest && mvn clean package -DskipTests'
                sh 'cd analytics-service && mvn clean package -DskipTests'
                sh 'cd audit-service && mvn clean package -DskipTests'
                sh 'cd ws && mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh 'docker-compose down'
                sh 'docker-compose up --build -d'
            }
        }
    }
}