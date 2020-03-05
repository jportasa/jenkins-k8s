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
        PROJECT = "REPLACE_WITH_YOUR_PROJECT_ID"
        APP_NAME = "gceme"
        FE_SVC_NAME = "${APP_NAME}-frontend"
        CLUSTER = "jenkins-cd"
        CLUSTER_ZONE = "us-east1-d"
        IMAGE_TAG = "gcr.io/${PROJECT}/${APP_NAME}:${env.BRANCH_NAME}.${env.BUILD_NUMBER}"
        JENKINS_CRED = "${PROJECT}"
    }
    stages {
        stage('Run unit tests') {
            //when { branch 'PR-*'}
            steps {
                // The needed steps for your testing
                container('busybox') {
                    sh """
                        echo 'Hola"
                        echo $APROJECT
                     """
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

        stage('Deployment to PRO') {
            steps {
                 container('helm') {
                    // Init authentication and config for your kubernetes cluster
                    sh "helm upgrade --install --wait prod-my-app ./helm --namespace pro"
                 }
            }
        }
    }
}