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
            sh '''echo "build on Java8 enviornment - Centos"
sh ./jenkins/build.sh > Pipeline
javac ./jenkins/build.java

'''
            stash(name: 'Java8', includes: 'Pipeline')
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

    stage('Java 8 Frontend test') {
      parallel {
        stage('Java 8 Frontend test') {
          agent {
            node {
              label 'Java8'
            }

          }
          steps {
            unstash 'Java8'
            sh '''sh pwd
sh pwd/Java8'''
          }
        }

        stage('Java 7 Frontend test') {
          steps {
            unstash 'Java8'
          }
        }

      }
    }

  }
}