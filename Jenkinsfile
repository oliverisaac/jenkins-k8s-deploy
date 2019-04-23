#!/usr/bin/env groovy

pipeline {
    agent {
        kubernetes {
            label 'jdk11'
        }
    }
    stages {
        stage('Checkout') {
            steps {
                checkout scm
            }
        }
        stage('Deploy Kubernetes') {
            steps {
                kubernetesDeploy(
                    kubeconfigId: 'bushelops-jenkins',               // REQUIRED

                    configs: 'deploys/basic-app/*.yaml', // REQUIRED
                    enableConfigSubstitution: true,
                )
            }
        }
    }
}
