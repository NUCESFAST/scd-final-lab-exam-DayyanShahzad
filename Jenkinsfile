pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git url: 'https://github.com/NUCESFAST/scd-final-lab-exam-DayyanShahzad.git', branch: 'master'
            }
        }
        stage('Build Frontend Image') {
            steps {
                dir('client') {
                    sh 'docker build -t $DOCKERHUB_REPO/frontend:$BUILD_NUMBER .'
                }
            }
        }
        stage('Build Backend Images') {
            parallel {
                stage('Build Auth') {
                    steps {
                        dir('auth') {
                            sh 'docker build -t $DOCKERHUB_REPO/auth:$BUILD_NUMBER .'
                        }
                    }
                }
                stage('Build Classrooms') {
                    steps {
                        dir('classrooms') {
                            sh 'docker build -t $DOCKERHUB_REPO/classrooms:$BUILD_NUMBER .'
                        }
                    }
                }
                stage('Build Event-bus') {
                    steps {
                        dir('event-bus') {
                            sh 'docker build -t $DOCKERHUB_REPO/event-bus:$BUILD_NUMBER .'
                        }
                    }
                }
                stage('Build Post') {
                    steps {
                        dir('post') {
                            sh 'docker build -t $DOCKERHUB_REPO/post:$BUILD_NUMBER .'
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
