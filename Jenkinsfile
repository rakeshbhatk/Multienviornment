pipeline {
  agent {
    node {
      label 'master'
    }

  }
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
            sh '''echo "build on Java8 enviornment - Centos"
sh ./jenkins/build.sh > Pipeline
javac ./jenkins/build.java

'''
            stash(name: 'Java8', includes: 'jenkins/**')
            archiveArtifacts 'Pipeline'
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

    stage('Java 7 Frontend test') {
      parallel {
        stage('Java 7 Front-end testing') {
          agent {
            node {
              label 'master'
            }

          }
          steps {
            dir(path: 'Java8') {
              unstash 'Java8'
            }

            sh 'ls'
          }
        }

        stage('Java 8 Front-end testing') {
          agent {
            node {
              label 'Java8'
            }

          }
          steps {
            dir(path: 'Java8') {
              unstash 'Java8'
            }

            sh '''javac ./Java8/jenkins/build.java 
'''
          }
        }

        stage('Java 7 performance test') {
          steps {
            unstash 'Java8'
          }
        }

      }
    }

  }
}