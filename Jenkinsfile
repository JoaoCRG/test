pipeline {
    agent any

    parameters {
        string(name: 'BUILD_NUMBER', defaultValue: '1', description: 'Incremental build number')
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    // Leitura do valor atual do BUILD_NUMBER de um arquivo (ou outro mecanismo)
                    def buildNumberFile = 'buildNumber.txt'
                    if (fileExists(buildNumberFile)) {
                        env.BUILD_NUMBER = readFile(buildNumberFile).trim()
                    } else {
                        env.BUILD_NUMBER = '1'
                    }
                    echo "NUMERO ATUAL: ${env.BUILD_NUMBER}"
                }
            }
        }

        stage('Increment') {
            steps {
                script {
                    // Incrementar o BUILD_NUMBER
                    def newBuildNumber = (env.BUILD_NUMBER.toInteger() + 1).toString()
                    writeFile(file: 'buildNumber.txt', text: newBuildNumber)
                    echo "NOVO NUMERO: ${newBuildNumber}"
                }
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/JoaoCRG/test'
            }
        }

        stage('Build') {
            steps {
                // Comandos para build
                echo "Building with BUILD_NUMBER: ${env.BUILD_NUMBER}"
            }
        }

        stage('Test') {
            steps {
                // Comandos para testes
                echo "Testing with BUILD_NUMBER: ${env.BUILD_NUMBER}"
            }
        }

        stage('Deploy') {
            steps {
                // Comandos para deploy
                echo "Deploying with BUILD_NUMBER: ${env.BUILD_NUMBER}"
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully!'
        }
        failure {
            echo 'Pipeline failed.'
        }
    }
}
