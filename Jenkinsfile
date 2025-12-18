pipeline {
    agent any
    environment {
        PORT = "${env.BRANCH_NAME == 'main' ? '8081' : env.BRANCH_NAME == 'Q1Branch' ? '8082' : '8083'}"
        CONTAINER_NAME = "web-container-${env.BRANCH_NAME}"
    }
    stages {
        stage('Cleanup') {
            steps {
                // Ensure existing container is stopped and removed before redeploying
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }
        stage('Deploy') {
            steps {
                // Use --user root only if necessary for initial setup, 
                // but generally aligning UID is more secure.
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
