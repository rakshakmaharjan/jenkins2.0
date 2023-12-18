pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh '''pwd
date'''
      }
    }

    stage('Test') {
      parallel {
        stage('Test') {
          steps {
            echo 'Test step'
          }
        }

        stage('Test-parallel') {
          steps {
            echo 'Test Parallel'
          }
        }

      }
    }

    stage('Deploy') {
      steps {
        echo 'Deploy'
        sleep 10
      }
    }

  }
}