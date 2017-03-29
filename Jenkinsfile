#!/usr/bin/env groovy
node('linux') {
    stage('Preparation') {
        // Delete node_modules folder in order to force installation every build.
        // This is necessary when swithcing Node versions, because of node_sass compilation.
        dir('node_modules') {
            deleteDir()
        }
        //checkout scm
        checkout([$class: 'GitSCM', branches: [[name: '**']], doGenerateSubmoduleConfigurations: false, extensions: [[$class: 'CleanBeforeCheckout']], submoduleCfg: [], userRemoteConfigs: [[credentialsId: 'jenkins', url: 'http://vgit.utv.lokal/scm/ui/dsb-bootstrap.git']]])
    }
    stage('Build') {
        // We're using nvm (node version manager) installed locally for the 'jenkins-agent' user.
        // The script below will make bash act as if it had been invoked as a login shell.
        // This way we will make use of ENV variables set in .bashrc etc.
        sh '''#!/bin/bash -l
        npm install
        '''
    }
    if ("${env.BRANCH_NAME}" == 'master') {
        stage('Deploy to Nexus') {
          sh '''#!/bin/bash -l
          npm version patch -m "Bump to version %s"
          '''
        }
    }
}