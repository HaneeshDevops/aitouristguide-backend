pipeline {
    agent any


    stages {
        stage('Build') {
            steps {
                // Checkout your source code from GitHub
                git 'https://github.com/HaneeshDevops/aitouristguide-backend.git'

                // Build your Spring Boot application

                withCredentials([usernamePassword(credentialsId: 'DockerRegistry', usernameVariable: 'DOCKER_USERNAME', passwordVariable: 'DOCKER_PASSWORD')]) {
                    sh "docker login -u ${DOCKER_USERNAME} -p ${DOCKER_PASSWORD}"

                    // Feedback Service
                    sh 'cd feedback-service'
                    sh 'mvn clean install -DskipTests'
                    sh 'docker build -t feedbackimage:latest .'
                    sh 'docker push haneeshdevops/feedbackimage:latest'
                    sh 'cd ..'

                    // Admin Service
                    sh 'cd admin-service'
                    sh 'mvn clean install -DskipTests'
                    sh 'docker build -t adminimage:latest .'
                    sh 'docker push haneeshdevops/adminimage:latest'
                    sh 'cd ..'

                    // Place Service
                    sh 'cd place-service'
                    sh 'mvn clean install -DskipTests'
                    sh 'docker build -t placeimage:latest .'
                    sh 'docker push haneeshdevops/placeimage:latest'
                    sh 'cd ..'

                    // Server Registry
                    sh 'cd server-registry'
                    sh 'mvn clean install -DskipTests'
                    sh 'docker build -t serverimage:latest .'
                    sh 'docker push haneeshdevops/serverimage:latest'
                    sh 'cd ..'

                    // Tourplan Service
                    sh 'cd tourplan-service'
                    sh 'mvn clean install -DskipTests'
                    sh 'docker build  -t tourplanimage:latest .'
                    sh 'docker push haneeshdevops/tourplanimage:latest'
                    sh 'cd ..'

                    // User Service
                    sh 'cd UserService'
                    sh 'mvn clean install -DskipTests'
                    sh 'docker build  -t userimage:latest .'
                    sh 'docker push haneeshdevops/userimage:latest'
                    sh 'cd ..'

                  // Launch all apps
                    sh 'docker-compose up -d'
                }
            }
        }
    }
}
