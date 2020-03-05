pipeline {
    agent {
        kubernetes {
            label 'jenkins-slave'
            yamlFile 'JenkinsKubernetesPod.yaml'
        }
    }
    environment {
        APP_NAME = 'python-quickstart'
        DOCKER_REGISTRY_ORG = 'jportasa'
    }
    stages {
        stage('Run unit tests') {
            //when {
            //    branch 'PR-*'
            //}
            steps {
                // The needed steps for your testing
                container('docker') {
                    sh 'docker images'
                    sh 'echo $APP_NAME'
               }
            }
        }

        stage('Build') {
            steps {
                // Build the app
                container('docker') {
                    sh 'docker images'
                }
            }
        }

        stage('Docker push') {
            steps {
                // Publish a docker image for your application
                container('docker') {
                    sh 'docker images'
                }
            }
        }

        stage('Deployment') {
            steps {
                script {
                    container('helm') {
                      // Init authentication and config for your kubernetes cluster
                      sh("helm init --client-only --skip-refresh")
                      sh("helm upgrade --install --wait prod-my-app ./helm --namespace pro")
                    }
                }
            }
        }
    }
}