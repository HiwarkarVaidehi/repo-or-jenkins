pipeline {
    agent any
    stages {
        stage('Checkout Code') {
            steps {
                git branch: 'main', url: 'https://github.com/HiwarkarVaidehi/repo-or-jenkins.git'
            }
        }
        stage('Build Docker Image') {
            steps {
                script {
                    dockerImage = docker.build('vaidehihiwarkar/your-app')
                }
            }
        }
        stage('Push Docker Image') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', 'my-docker-id') {
                        dockerImage.push()
                    }
                }
            }
        }
       stage('Deploy') {
            steps {
                sshPublisher(
                    publishers: [sshPublisherDesc(
                        configName: 'EC2-server',
                        transfers: [sshTransfer(
                            sourceFiles: '',
                            execCommand: 'docker run -d -p 80:3000 vaidehihiwarkar/your-app'
                        )]
                    )]
                )
            }
        }
}
}
