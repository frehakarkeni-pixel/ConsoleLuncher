
pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                echo 'Recuperation du projet depuis GitHub'
                checkout scm
            }
        }

        stage('Build') {
            steps {
                echo 'Compilation et generation du fichier WAR'
                sh 'mvn clean package'
            }
        }

        stage('Tests') {
            steps {
                echo 'Execution des tests unitaires'
                sh 'mvn test'
            }
        }

        stage('Build Docker') {
            steps {
                echo 'Construction de l image Docker'
                sh 'docker build -t java-web-app:latest .'
            }
        }

        stage('Deploy Docker Swarm') {
            steps {
                echo 'Deploiement de l application avec Docker Swarm'
                sh 'docker service update --image java-web-app:latest java-web-app'
            }
        }
    }
}


