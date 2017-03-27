#!/usr/bin/env groovy
node('linux') {
   stage('Preparation') {
      checkout scm
      gitCmd = 'git remote set-url origin ${env.GIT_REPO_URL}'
      echo gitCmd
      //sh 'git remote set-url origin ${bamboo.repository.git.repositoryUrl}'
   }
   stage('Build') {
      // We're using nvm (node version manager) installed locally for the 'jenkins-agent' user.
      // The script below will make bash act as if it had been invoked as a login shell.
      // This way we will make use of ENV variables set in .bashrc etc.
      //sh '''#!/bin/bash -l
      //npm install
      //'''
   }
   stage('Deploy to Nexus') {
      //sh '''#!/bin/bash -l
      //npm version patch -m "Bump to version %s"
      //'''
   }
}