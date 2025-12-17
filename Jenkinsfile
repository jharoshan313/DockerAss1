pipeline{
    
    agent{
        label {
            label 'built-in'
            customWorkSpace '/mnt/docker-assignment1'
        }
    }

    stages {
             
             stage(Stage1) {

                steps{
                     
                     sh 'rm -rf *'
                     sh 'chmod -R 777 /mnt/docker-assignment1' 
                     sh 'sudo yum install docker -y'
                     sh 'sudo systemctl start docker'
                     sh 'docker pull httpd'
                     sh 'docker run --name c1 -dp 80:80 httpd'
                     sh 'docker cp /mnt/docker-assignment/DockerAss1/index.html c1:/usr/local/apache2/htdoc'
                     sh 'docker run --name c2 -dp 90:80 httpd'
                     sh 'docker cp /mnt/docker-assignment/DockerAss1/index.html c2:/usr/local/apache2/htdoc'
                     sh 'docker run --name c2 -dp 8080:80 httpd'
                     sh 'docker cp /mnt/docker-assignment/DockerAss1/index.html c3:/usr/local/apache2/htdoc'




                }


             }



    }





}
