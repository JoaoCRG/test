pipeline {
    agent any

    environment {
        // Definindo a hora específica desejada (4h da manhã)
        DESIRED_HOUR = '04:00'
        // Arquivo para armazenar a data da última execução que fez o pull request
        LAST_PULL_FILE = 'last_pull_date.txt'
        // Obtendo a data atual da execução do job
        CURRENT_DATE = ''
        // Definindo a hora atual da execução do job
        CURRENT_HOUR = ''
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    // Obtendo a data e a hora atuais
                    CURRENT_DATE = sh(script: 'date "+%Y-%m-%d"', returnStdout: true).trim()
                    CURRENT_HOUR = sh(script: 'date "+%H:%M"', returnStdout: true).trim()
                    echo "Current date: ${CURRENT_DATE}, Current hour: ${CURRENT_HOUR}"
                }
            }
        }

        stage('Check Last Pull Date') {
            steps {
                script {
                    // Lendo a data da última execução que fez o pull request
                    def lastPullDate = ''
                    if (fileExists(LAST_PULL_FILE)) {
                        lastPullDate = readFile(LAST_PULL_FILE).trim()
                    }

                    echo "Last pull request date: ${lastPullDate}"

                    // Verificando se a data atual é diferente da data da última execução que fez o pull request
                    if (CURRENT_DATE != lastPullDate && CURRENT_HOUR >= DESIRED_HOUR) {
                        // Realizar o pull request
                        echo "Making pull request..."
                        // Coloque aqui os comandos para fazer o pull request

                        // Atualizando a data da última execução que fez o pull request
                        writeFile(file: LAST_PULL_FILE, text: CURRENT_DATE)
                    } else {
                        // Não realizar o pull request
                        echo "Skipping pull request."
                    }
                }
            }
        }

        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/JoaoCRG/test'
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
