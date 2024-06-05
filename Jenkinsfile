pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                git 'https://github.com/NUCESFAST/scd-final-lab-exam-DayyanShahzad.git'
            }
        }
        
        stage('Build Frontend Image') {
            steps {
                dir('client') {
                    bat 'start /B build-frontend.bat' // Assuming a batch script for building the frontend
                }
            }
        }
        
        stage('Build Backend Images') {
            parallel {
                stage('Build Auth') {
                    steps {
                        dir('auth') {
                            bat 'start /B build-auth.bat' // Assuming a batch script for building the auth service
                        }
                    }
                }
                stage('Build Classrooms') {
                    steps {
                        dir('classrooms') {
                            bat 'start /B build-classrooms.bat' // Assuming a batch script for building the classrooms service
                        }
                    }
                }
                stage('Build Event-bus') {
                    steps {
                        dir('event-bus') {
                            bat 'start /B build-event-bus.bat' // Assuming a batch script for building the event-bus service
                        }
                    }
                }
                stage('Build Post') {
                    steps {
                        dir('post') {
                            bat 'start /B build-post.bat' // Assuming a batch script for building the post service
                        }
                    }
                }
            }
        }

        stage('Push Images to Docker Hub') {
            steps {
                script {
                    // Add commands for pushing Docker images
                    bat 'docker login -u your-username -p your-password'
                    bat 'docker push your-image'
                }
            }
        }
    }

    post {
        always {
            cleanWs()
        }
    }
}
