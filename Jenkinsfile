pipeline {
    agent {
        kubernetes {
            label 'jenkins-slave'  // all your pods will be named with this prefix, followed by a unique id
            yamlFile 'JenkinsKubernetesPod.yaml'
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
    }
}