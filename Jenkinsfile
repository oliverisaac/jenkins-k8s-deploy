#!/usr/bin/env groovy

import hudson.model.*

node('master'){
    label: 'jdk11'

    kubernetesDeploy(
        kubeconfigId: 'bushelops-jenkins',               // REQUIRED

        configs: 'deploys/basic-app/*.yaml', // REQUIRED
        enableConfigSubstitution: true,
    )
}
