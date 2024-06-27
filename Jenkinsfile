pipeline {
    agent any

    environment {
		GITHUB_TOKEN= credentials('github-pat')
        MAVEN_OPTS = '-Dmaven.test.failure.ignore=true'
    }

    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/usuqintess/nosqlrel.git', branch: 'main',
                credentialsId:"${env.GITHUB_TOKEN}"
            }
        }

        stage('Compile') {
            steps {
                script {
                    bat 'mvn clean compile'
                }
            }
        }

        stage('Test') {
            steps {
                // Executar testes
                script {
                    bat 'mvn test'
                }
            }
        }

        stage('Build') {
            steps {
                // Fazer o build do projeto
                script {
                    bat 'mvn package'
                }
            }
        }

        stage('Deploy') {
            steps {
                script {
                    bat 'mvn deploy'
                }
            }
        }
    }

    post {
        always {
            echo 'Pipeline finished.'
        }
        success {
            echo 'Pipeline succeeded!'
        }
        failure {
            echo 'Pipeline failed!'
        }
    }
}
