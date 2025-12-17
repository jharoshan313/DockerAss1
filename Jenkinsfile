pipeline {
    agent any
    environment {
        PORT = "${env.BRANCH_NAME == 'main' ? '8081' : env.BRANCH_NAME == 'dev' ? '8082' : '8083'}"
        CONTAINER_NAME = "web-container-${env.BRANCH_NAME}"
    }
    stages {
        stage('Cleanup') {
            steps {
                sh "docker rm -f ${CONTAINER_NAME} || true"
            }
        }
        stage('Fix Permissions & Deploy') {
            steps {
                // 1. Grant read permissions so the container's web user can access the file
                sh "chmod 644 ${WORKSPACE}/index.html"
                
                // 2. Run the container
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
