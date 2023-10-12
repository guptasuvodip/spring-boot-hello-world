pipeline {
    agent any
    // agent {
    //     label 'mv' # for agent need to add lebel of the node then it will work.
    // }
    environment {
        CI = true
        ARTIFACTORY_ACCESS_TOKEN = credentials('artifactory-access-token')
        JFROG_PASSWORD = credentials('jfrog-password')
    }
    stages {
        stage('Checkout Git repository') {
            steps {
                // Checkout your source code from your version control system (e.g., Git)
                git branch: 'artifact' , url : 'https://github.com/guptasuvodip/spring-boot-hello-world.git'
            }
        }
        stage('Upload to Artifactory') {
              script {
                      // Define the Docker image and access token
                      def dockerImage = 'releases-docker.jfrog.io/jfrog/jfrog-cli-v2:2.2.0'
                      def accessToken = env.ARTIFACTORY_ACCESS_TOKEN

                      // Run the JFrog CLI command within a Docker container
                      sh """
                        docker run --rm \\
                        -e ARTIFACTORY_ACCESS_TOKEN=${accessToken} \\
                        -v ${WORKSPACE}:/workspace \\
                        ${dockerImage} \\
                        jfrog rt upload --url http://192.168.1.230:8082/artifactory/ /workspace/target/demo-0.0.1-SNAPSHOT.jar java-web-app/
                        """
            }
        }
            
    }
        
}
    
