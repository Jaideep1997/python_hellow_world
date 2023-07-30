pipeline {
    agent any
    stages {
        stage('Git Clone') {
            steps {
                git branch: 'main', credentialsId: 'b5f1127e-37e3-49c4-a214-4dc4b128622a', url: 'https://github.com/Jaideep1997/python_hellow_world.git'
            }
        }
        
        // Building Docker images
        stage('Building image') {
            steps {
                script {
                    def containerName = "nostalgic_nash" // Updated container name
                    
                    // Stop and remove the container if it's running (suppress errors)
                    sh "docker stop ${containerName} || true"
                    sh "docker rm ${containerName} || true"
                    
                    // Build and run the Docker image
                    docker.build("jaideep205/python-hello_world", ".") // Removed space between image name and dot
                    docker.image("jaideep205/python-hello_world").run("-d -p 3030:3000 --name ${containerName} --rm")
                }
            }
        }
        
        // Dockerhub login and push
        stage('Dockerhub login and push') {
            steps {
                withCredentials([string(credentialsId: '342b817e-9129-4cdd-a815-c6e313c07ee2', variable: 'dockerpwd')]) {
                    sh "docker login -u jaideep205 -p ${dockerpwd}"
                }
                sh "docker push jaideep205/python-hello_world"
            }
        }
    }
}
