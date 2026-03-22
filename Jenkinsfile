pipeline {
    agent any

    tools {
        // These MUST match the names you typed in 'Manage Jenkins > Tools'
        maven 'maven3'
        jdk 'jdk21'
    }

    stages {
        stage('Checkout SCM') {
            steps {
                // This pulls the code from your local folder into Jenkins' workspace
                checkout scm
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean compile'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }

        stage('Package') {
            steps {
                sh 'mvn package'
            }
        }

        stage('Run Application') {
            steps {
                // Runs the jar and kills it after 15 seconds so the build finishes
                sh 'timeout 15 java -jar target/maven2023-1.0-SNAPSHOT.jar'
            }
        }
    }

    post {
        success {
            echo 'Build Successful - LEGO Set is Complete!'
        }
        failure {
            echo 'Build Failed - Check your code or tests.'
        }
    }
}
