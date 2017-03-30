#!/usr/bin/env groovy
node('linux') {
    def lastCommit1 = sh returnStdout: true, script: 'git log -1 --pretty=%B'
    echo "$lastCommit1"
    if (lastCommit1.startsWith("Bump to version")) {
        return
    }
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
    //Beacuse "npm version patch" will commit and push to master, this hack is applied to avoid building indefinitely.
    def lastCommit = sh returnStdout: true, script: 'git log -1 --pretty=%B'
    if ("${env.BRANCH_NAME}" == 'master' && !lastCommit.startsWith("Bump to version")) {
        stage('Deploy to Nexus') {
          sh '''#!/bin/bash -l
          npm version patch -m "Bump to version %s"
          '''
        }
    }
}