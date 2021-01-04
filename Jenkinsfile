pipeline {
  agent {
    docker {
      label 'dockerhost-label'
      image 'quay.io/ansible/molecule:3.2.0a0'
      args '-v /var/run/docker.sock:/var/run/docker.sock -u root'
    }
  }
  stages {

    stage ('Get the latest code') {
      steps {
        dir('mywebapp') {
          git 'https://github.com/r3dl0ck/mywebapp.git'
        }
      }
    }

    stage ('Install dependencies') {
      steps {
        sh '''
          apk update
          apk add bash
        '''
      }
    }

    stage ('Molecule test') {
      steps {
        sh '''
          cd mywebapp
          molecule test --all
        '''
      }
    }

  } 

  post { 
    always { 
      cleanWs()
    }
  }

}
