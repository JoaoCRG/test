pipeline {
    agent any

    environment {
        // Definindo a hora específica desejada (3h da manhã)
        DESIRED_HOUR = '03:00'
        // Obtendo a hora atual da execução do job
        CURRENT_HOUR = ''
        // Definindo a diferença máxima em horas entre as duas horas (24 horas)
        MAX_HOURS_DIFF = 24
    }

    stages {
        stage('Set Current Time') {
            steps {
                script {
                            // Obtendo a hora atual e definindo-a na variável CURRENT_HOUR
                            CURRENT_HOUR = sh(script: 'date "+%H:%M"', returnStdout: true).trim()
                            echo "Current hour: ${CURRENT_HOUR}"
                        }
            }
        }

        stage('Check Time Difference') {
            steps {
                script {
                    // Calculando a diferença em horas entre as horas desejada e atual
                    def desiredTimestamp = $DESIRED_HOUR
                    def currentTimestamp = $CURRENT_HOU\" +\"%s\"", returnStdout: true).trim()
                    def timeDiff = (currentTimestamp.toInteger() - desiredTimestamp.toInteger()) / 3600

                    // Verificando se a diferença é maior que MAX_HOURS_DIFF
                    if (timeDiff > MAX_HOURS_DIFF) {
                        // Realizar o pull request
                        echo "Time difference is greater than ${MAX_HOURS_DIFF} hours. Making pull request..."
                        stage('Checkout') {
                                                            steps {
                                                                git branch: 'main', url: 'https://github.com/JoaoCRG/test'
                                                            }
                                                        }
                    } else {

                        echo "Time difference is within ${MAX_HOURS_DIFF} hours. Skipping pull request."
                    }
                }
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

stage('Checkout') {
                                    steps {
                                        git branch: 'main', url: 'https://seu-repositorio.git'
                                    }
                                }
