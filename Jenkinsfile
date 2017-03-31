#!/usr/bin/env groovy
node('linux') {
    stage('Preparation') {
        return
        // Delete node_modules folder in order to force installation on every build.
        // This is necessary when eg. swithcing Node versions, because of node_sass compilation etc..
        dir('node_modules') {
            deleteDir()
        }
        checkout scm
        //This check is applied to avoid building indefinitely.
        def lastCommit = sh returnStdout: true, script: 'git log -1 --pretty=%B'
        if (lastCommit.startsWith("[ci skip]")) {
            return;
        }
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
          npm version patch -m "[ci skip] Bump to version %s"
          '''
        }
    }
}