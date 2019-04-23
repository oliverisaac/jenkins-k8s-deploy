#!/usr/bin/env groovy

pipeline {
    agent {
        kubernetes {
            label 'jdk11'
        }
    }
    parameters {
        string(name: 'namespace', defaultValue: 'test-jenkins', description: 'Which namespace should we deploy to?')
        string(name: 'appname', defaultValue: 'cafe', description: 'Name of app')
        choice(
            name: 'context',
            choices: [
                'bushelops-dev-us-alpha',
                'bushelops-dev-us-beta',
            ],
            description: 'Kubernetes Target Context'
        )
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
                    kubeconfigId: "${params.context}",               // REQUIRED

                    configs: 'deploys/basic-app/*.yaml', // REQUIRED
                    enableConfigSubstitution: true,
                )
            }
        }
    }
}
