pipeline {

    agent any

    environment {
        IMAGE_TAG = "${BUILD_NUMBER}"
        IMAGE_NAME = "manishh98/jenkins-python-app"
    }

    stages {

        stage('Checkout Application Code') {
            steps {
                git credentialsId: 'github-creds',
                    url: 'https://github.com/manishh98/jenkins-python-argocd-k8s.git',
                    branch: 'main'
            }
        }

        stage('Build Docker Image') {
            steps {
                sh '''
                docker build -t ${IMAGE_NAME}:${IMAGE_TAG} .
                '''
            }
        }

        stage('Docker Login & Push Image') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'docker-creds',
                    usernameVariable: 'DOCKER_USER',
                    passwordVariable: 'DOCKER_PASS'
                )]) {
                    sh '''
                    echo "$DOCKER_PASS" | docker login -u "$DOCKER_USER" --password-stdin
                    docker push ${IMAGE_NAME}:${IMAGE_TAG}
                    '''
                }
            }
        }

        stage('Checkout K8s Manifests Repo') {
            steps {
                git credentialsId: 'github-creds',
                    url: 'https://github.com/manishh98/jenkins-k8s-manifests.git',
                    branch: 'main'
            }
        }

        stage('Update Image Tag & Push Manifest') {
            steps {
                withCredentials([usernamePassword(
                    credentialsId: 'github-creds',
                    usernameVariable: 'GIT_USER',
                    passwordVariable: 'GIT_PASS'
                )]) {
                    sh '''
                    sed -i "s|image:.*|image: ${IMAGE_NAME}:${IMAGE_TAG}|" deploy.yaml
                    git add deploy.yaml
                    git commit -m "Update image tag to ${IMAGE_TAG}"
                    git push https://${GIT_USER}:${GIT_PASS}@github.com/manishh98/jenkins-k8s-manifests.git main
                    '''
                }
            }
        }
    }
}

