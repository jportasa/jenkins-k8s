pipeline {
    agent {
        kubernetes {
            label 'jenkins-slave'  // all your pods will be named with this prefix, followed by a unique id
            yamlFile 'JenkinsKubernetesPod.yaml'
            defaultContainer 'jnlp'
            idleMinutes 5  // how long the pod will live after no jobs have run on it
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
                container('busybox') {
                    sh 'echo "Hola"'
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