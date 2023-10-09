pipeline {
    agent any
    // agent {
    //     label 'mv' # for agent need to add lebel of the node then it will work.
    // }
    tools {
        maven 'mvn'
        jdk 'jdk:11'
    }
    environment {
        scannerHome = tool 'sonar-scanner'
    }
    stages {
        stage('SCM') {
            steps {
                // Checkout your source code from your version control system (e.g., Git)
                checkout scm
            }
        }
        stage('SonarQube Analysis') {
            steps {
                script {
                    // Run SonarQube analysis
                    withSonarQubeEnv('sonarserver') {
                        sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectName=project-app -Dsonar.projectKey=project-app -Dsonar.java.binaries=src/main/java"
                    }
                }
            }
        }
}
