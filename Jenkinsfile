pipeline {
    agent any

    tools {
        maven 'Maven_3'
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn clean install'
            }
        }

        stage('Performance Test') {
            steps {
                bat 'jmeter -n -t tests/performance/demo.jmx -l result.jtl'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'result.jtl', allowEmptyArchive: true
        }
    }
}