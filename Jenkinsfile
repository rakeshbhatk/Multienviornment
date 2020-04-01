pipeline {
  agent any
  stages {
    stage('Java8') {
      parallel {
        stage('Java8') {
          agent {
            node {
              label 'Java8'
            }

          }
          steps {
            sh 'echo "build on Java8 enviornment - Centos"'
          }
        }

        stage('Java7') {
          agent {
            node {
              label 'master'
            }

          }
          steps {
            bat 'echo "Building on Java7 master node"'
          }
        }

      }
    }

  }
}