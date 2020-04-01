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
            sh '''echo "build on Java8 enviornment - Centos" > Pipeline
sh ./jenkins/build.sh
'''
            stash(name: 'File', includes: '*.sh')
          }
        }

        stage('Java7') {
          agent any
          steps {
            sh 'echo "running on master building on java7"'
          }
        }

      }
    }

    stage('Test Step') {
      steps {
        unstash 'tmpPipeline'
      }
    }

  }
}