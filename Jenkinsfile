pipeline {
    agent any

    stages {
        stage('Clone Repository') {
            steps {
                // Clone the repository with the specified branch and credentials
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/tamil2303a/DevOne.git'
            }
        }
        
        stage('Build Docker Image') {
            steps {
                // Build the Docker image from the current directory
                sh 'docker build -t dodge:latest .'
            }
        }
        
        stage('Run Docker Container') {
            steps {
                script {
                    // Check if a container named 'foodyy' already exists, and remove it if it does
                    def containerExists = sh(script: "docker ps -q -f name=foodyy", returnStdout: true).trim()
                    if (containerExists) {
                        sh 'docker stop charger'
                        sh 'docker rm charger'
                    }
                }
                // Run the Docker container with the specified options
                sh 'docker run -itd --name charger -p 8083:80 dodge:latest'
            }
        }
    }
}
