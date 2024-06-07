pipeline {
    agent any

    environment {

        DESIRED_HOUR = '04:00'
        LAST_PULL_FILE = 'last_pull_date.txt'
        CURRENT_DATE = ''
        CURRENT_HOUR = ''
    }

    stages {
        stage('Initialize') {
            steps {
                script {
                    CURRENT_DATE = sh(script: 'date "+%Y-%m-%d"', returnStdout: true).trim()
                    CURRENT_HOUR = sh(script: 'date "+%H:%M"', returnStdout: true).trim()
                    echo "Current date: ${CURRENT_DATE}, Current hour: ${CURRENT_HOUR}"
                }
            }
        }

        stage('Check Last Pull Date') {
            steps {
                script {
                    def lastPullDate = ''
                    if (fileExists(LAST_PULL_FILE)) {
                        lastPullDate = readFile(LAST_PULL_FILE).trim()
                    }

                    echo "Last pull request date: ${lastPullDate}"

                    if (CURRENT_DATE != lastPullDate && CURRENT_HOUR >= DESIRED_HOUR) {
                        echo "Making pull request..."
                        writeFile(file: LAST_PULL_FILE, text: CURRENT_DATE)
                    } else {
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
