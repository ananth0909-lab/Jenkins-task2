pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'chmod +x build.sh'
                sh './build.sh'
            }
        }
    }

    post {
        success {
            emailext (
                subject: "SUCCESS: Job ${env.JOB_NAME}",
                body: """Build Successful!

Job: ${env.JOB_NAME}
Build Number: ${env.BUILD_NUMBER}
Build URL: ${env.BUILD_URL}
""",
                to: "your-email@gmail.com"
            )
        }

        failure {
            emailext (
                subject: "FAILED: Job ${env.JOB_NAME}",
                body: "Build Failed. Check console output.",
                to: "your-email@gmail.com"
            )
        }
    }
}
