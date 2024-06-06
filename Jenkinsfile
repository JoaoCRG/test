pipeline {
    agent any

    environment {

        DESIRED_HOUR = '03:00'
        CURRENT_HOUR = ''
        MAX_HOURS_DIFF = 24
    }

    stages {
        stage('Set Current Time') {
            steps {
                script {
                    CURRENT_HOUR = sh(script: 'date "+%H:%M"', returnStdout: true).trim()
                    echo "Current hour: ${CURRENT_HOUR}"
                }
            }
        }

        stage('Check Time Difference') {
            steps {
                script {
                    def timeDiff = sh(script: "echo $(( (\$(date -d \"$DESIRED_HOUR\" +\"%s\") - \$(date -d \"$CURRENT_HOUR\" +\"%s\")) / 3600 ))", returnStdout: true).trim().toInteger()


                    if (timeDiff > MAX_HOURS_DIFF) {
                        // Realizar o pull request
                        echo "Time difference is greater than ${MAX_HOURS_DIFF} hours. Making pull request..."

                         stage('Checkout') {
                                    steps {
                                        git branch: 'main', url: 'https://seu-repositorio.git'
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
