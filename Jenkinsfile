#!/usr/bin/env groovy

pipeline {
    agent {
        kubernetes {
        }
    }

    parameters {
        string(name: 'namespace', defaultValue: 'test-jenkins', description: 'Which namespace should we deploy to?')
        string(name: 'appname', defaultValue: 'cafe', description: 'Name of app')
        string(name: 'context', defaultValue: '', description: 'Jenkins Kubernetes credentials to use')
        string(name: 'appType', defaultValue: 'basic-app', description: 'Type of app to deploy')
    }

    environment {
        NAMESPACE = "${params.namespace}"
        APP_NAME = "${params.appname}"
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
                    kubeconfigId: "${params.context}",
                    configs: "deploys/${params.appType}/*.yaml",

                    enableConfigSubstitution: true,
                )
            }
        }
    }
}
