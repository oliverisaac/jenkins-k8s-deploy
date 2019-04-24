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
        string(name: 'TLD', defaultValue: '', description: 'Ingress TLD to use.')
        string(name: 'ingressClass', defaultValue: 'external', description: 'nginx ingress class to use')
    }

    // environment is used in the kubernetes yaml files for templating
    environment {
        NAMESPACE = "${params.namespace}"
        APP_NAME = "${params.appname}"
        TLD = "${params.TLD}"
        INGRESS_CLASS = "${params.ingressClass}"
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
