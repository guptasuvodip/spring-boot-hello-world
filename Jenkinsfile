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
        stage('Upload to Artifactory') {
            steps {
                script {
                    // Define the Docker image and access token
                    def dockerImage = 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0'
                    def accessToken = env.ARTIFACTORY_ACCESS_TOKEN

                    // Run the JFrog CLI command within a Docker container
                    sh """
                    docker run --rm \\
                    -e ARTIFACTORY_ACCESS_TOKEN=${accessToken} \\
                    -v \${WORKSPACE}:/workspace \\
                    ${dockerImage} \\
                    jfrog rt upload --url http://192.168.1.230:8082/ /workspace/target/demo-1.0.2-SNAPSHOT.jar artifactory/
                    """
                }
            }
        }
    }
}
