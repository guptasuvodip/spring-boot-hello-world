pipeline {
    agent any
    tools {
        // Define the 'maven-class' tool and 'jdk:17' tool
        maven 'maven-class'
        jdk 'jdk:17'
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
                // Define the Maven tool (assuming 'Default Maven' is a configured tool)
                script {
                    def mvn = tool 'Default Maven'
                    // Run SonarQube analysis with Maven
                    withSonarQubeEnv('sonarserver') {
                        sh "${mvn}/bin/mvn clean verify sonar:sonar -Dsonar.projectKey=project-app -Dsonar.projectName='project-app'"
                    }
                }
            }
        }
    }
}
