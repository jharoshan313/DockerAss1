pipeline {
        agent {
        label {
            label 'built-in'
        }
    }
    environment {
        // Dynamically set port based on branch name
        PORT = "${env.BRANCH_NAME == 'main' ? '8081' : env.BRANCH_NAME == 'Q1Branch' ? '8082' : '8083'}"
        CONTAINER_NAME = "web-container-${env.BRANCH_NAME}"
    }
    stages {
        stage('Cleanup') {
            steps {
                // Remove existing container if it exists
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }
        stage('Deploy to Docker') {
            steps {
                // Run httpd image, mounting the branch's index.html to the web server path
                sh """
                docker run -d \
                    --name ${CONTAINER_NAME} \
                    -p ${PORT}:80 \
                    -v ${WORKSPACE}/index.html:/usr/local/apache2/htdocs/index.html:ro \
                    httpd:latest
                """
            }
        }
    }
}
