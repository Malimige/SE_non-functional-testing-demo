pipeline {
    agent any

    environment {
        JAVA_HOME = 'C:\\Program Files\\Eclipse Adoptium\\jdk-17.0.17.10-hotspot'
        MAVEN_HOME = 'C:\\Program Files\\Maven\\apache-maven-3.9.12'
        JMETER_HOME = 'C:\\Tools\\apache-jmeter-5.6.3'
        PATH = "${JAVA_HOME}\\bin;${MAVEN_HOME}\\bin;${JMETER_HOME}\\bin;${env.PATH}"
    }

    stages {
        stage('Build') {
            steps {
                bat 'java -version'
                bat 'mvn -version'
                bat 'mvn clean install'
            }
        }

        stage('Performance Test') {
            steps {
                bat '"%JMETER_HOME%\\bin\\jmeter.bat" -n -t tests/performance/demo.jmx -l result.jtl'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: 'result.jtl', allowEmptyArchive: true
        }
    }
}