pipeline {
    agent any
    environment {
        CI = true
        ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
        JFROG_PASSWORD = credentials('jfrog-password')
    }
    stages {
        stage('Checkout Git repository') {
            steps {
                script {
                    // Checkout your source code from your version control system (e.g., Git)
                    git branch: 'artifact', url: 'https://github.com/guptasuvodip/spring-boot-hello-world.git'
                }
            }
        }
        stage('Build and Run Spring Boot Application') {
            steps {
                script {
                    // Assuming you are inside the project directory, you can use Maven to run the Spring Boot application
                    sh 'mvn spring-boot:run'
                }
            }
        }
        stage('Build JAR') {
            steps {
                script {
                    // Use Maven to build the JAR file
                    sh 'mvn clean install'
                }
            }
        }
        stage('Execute JAR') {
            steps {
                script {
                    // After building the JAR, execute it
                    sh 'java -jar target/spring-boot-hello-world-1.0.2-SNAPSHOT.jar'
                }
            }
        }
        stage('Upload to Artifactory') {
            steps {
                script {
                    // Define the Docker image and access token
                    def dockerImage = 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0'
                    def accessToken = env.ARTIFACTORY_ACCESS_TOKEN

                    // Run the JFrog CLI command within a Docker container to upload the JAR
                    sh """
                    docker run --rm \\
                    -e ARTIFACTORY_ACCESS_TOKEN=${accessToken} \\
                    -v \${WORKSPACE}:/workspace \\
                    ${dockerImage} \\
                    jfrog rt upload --url http://54.144.143.2:8082 /workspace/target/spring-boot-hello-world-1.0.2-SNAPSHOT.jar artifact/
                    """
                }
            }
        }
    }
}
