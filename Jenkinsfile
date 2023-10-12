pipeline {
    agent any
    // agent {
    //     label 'mv' # for agent need to add lebel of the node then it will work.
    // }
    environment {
        CI = true
        ARTIFACTORY_ACCESS_TOKEN = credentials()
        JFROG_PASSWORD = credentials()
    }
    stages {
        stage('Checkout Git repository') {
            steps {
                // Checkout your source code from your version control system (e.g., Git)
                git branch: 'artifact' , url : 'https://github.com/guptasuvodip/spring-boot-hello-world.git'
            }
        }
        
                }
            }
        }
    }
}
