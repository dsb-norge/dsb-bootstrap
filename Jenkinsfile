#!/usr/bin/env groovy
node('linux') {
    stage('Preparation') {
        // Delete node_modules folder in order to force installation every build.
        // This is necessary when swithcing Node versions, because of node_sass compilation.
        dir('node_modules') {
            deleteDir()
        }
        checkout scm
    }
    stage('Build') {
        // We're using nvm (node version manager) installed locally for the 'jenkins-agent' user.
        // The script below will make bash act as if it had been invoked as a login shell.
        // This way we will make use of ENV variables set in .bashrc etc.
        sh '''#!/bin/bash -l
        npm install
        '''
    }
    lastCommit = sh returnStdout: true, script: 'git log -1 --pretty=%B'
    if ("${env.BRANCH_NAME}" == 'master' && !lastCommit.startsWith("Bump to version")) {
        echo "Deploying to Nexus..."
        //stage('Deploy to Nexus') {
        //  sh '''#!/bin/bash -l
        //  npm version patch -m "Bump to version %s"
        //  '''
        //}
    }
}