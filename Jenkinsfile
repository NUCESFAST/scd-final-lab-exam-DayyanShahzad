pipeline {
    agent any

    environment {
        DOCKER_CREDENTIALS_ID = 'docker-hub'
        DOCKERHUB_REPO = 'your-dockerhub-username'
        REPO_NAME = 'your-repo-name'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/NaseemKhan005/react-bank-app.git'
            }
        }
        
        stage('Build Frontend Image') {
            steps {
                script {
                    dir('client') {
                        sh 'docker build -t $DOCKERHUB_REPO/frontend:$BUILD_NUMBER .'
                    }
                }
            }
        }
        
        stage('Build Backend Images') {
            parallel {
                stage('Build Auth') {
                    steps {
                        script {
                            dir('Auth') {
                                sh 'docker build -t $DOCKERHUB_REPO/auth:$BUILD_NUMBER .'
                            }
                        }
                    }
                }
                stage('Build Classrooms') {
                    steps {
                        script {
                            dir('Classrooms') {
                                sh 'docker build -t $DOCKERHUB_REPO/classrooms:$BUILD_NUMBER .'
                            }
                        }
                    }
                }
                stage('Build Event-bus') {
                    steps {
                        script {
                            dir('event-bus') {
                                sh 'docker build -t $DOCKERHUB_REPO/event-bus:$BUILD_NUMBER .'
                            }
                        }
                    }
                }
                stage('Build Post') {
                    steps {
                        script {
                            dir('Post') {
                                sh 'docker build -t $DOCKERHUB_REPO/post:$BUILD_NUMBER .'
                            }
                        }
                    }
                }
            }
        }
        
        stage('Push Images to Docker Hub') {
            steps {
                script {
                    docker.withRegistry('https://index.docker.io/v1/', "$DOCKER_CREDENTIALS_ID") {
                        sh 'docker push $DOCKERHUB_REPO/frontend:$BUILD_NUMBER'
                        sh 'docker push $DOCKERHUB_REPO/auth:$BUILD_NUMBER'
                        sh 'docker push $DOCKERHUB_REPO/classrooms:$BUILD_NUMBER'
                        sh 'docker push $DOCKERHUB_REPO/event-bus:$BUILD_NUMBER'
                        sh 'docker push $DOCKERHUB_REPO/post:$BUILD_NUMBER'
                    }
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
