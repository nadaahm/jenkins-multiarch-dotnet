pipeline {
    agent any

    stages {
        stage('Checkout repo') {
            steps {
                echo 'Cloning repo from GitHub'
                git branch: 'main', url: 'https://github.com/nadaahm/jenkins-multiarch-dotnet'
                sh 'ls'
            }
        }
        stage('Build docker') {
            parallel {
                stage('docker build x86') {
                    agent {
                        label "x86"
                    }
                    steps {
                        sh 'docker build -t ahmednada/web-app-multiarch:manifest-amd64 --build-arg ARCH=amd64/ -f Dockerfile.alpine-x64 .'
                    }

                }
                stage('docker build arm64') {
                    agent {
                        label "arm64"
                    }
                    steps {
                        sh 'docker build -t ahmednada/web-app-multiarch:manifest-arm64v8 --build-arg ARCH=arm64v8/ -f Dockerfile.alpine-arm64 .'
                    }

                }
            }

        }
            
        stage('Create multiarch manifest') {
            steps {
                sh 'docker manifest create \
                ahmednada/web-app-multiarch:manifest-latest \
                --amend ahmednada/web-app-multiarch:manifest-amd64 \
                --amend ahmednada/web-app-multiarch:manifest-arm64v8 '
                echo 'manifest created'
                sh 'docker manifest push ahmednada/web-app-multiarch:manifest-latest'
            }
        }

    }
}