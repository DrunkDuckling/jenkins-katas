pipeline {
  agent any
  stages {
    stage('clone down'){
        steps{
          unstash(name: 'git push')

          stash (
          name: 'git push',
          allowEmpty: true,
          excludes: '.git'
          )
          sh 'echo "HEJ MED DIG"'
        }
    }
    stage('Say Hello') {
      parallel {
        stage('Parallel execution') {
          steps {
            sh 'echo "hello world"'
          }
        }

        stage('build app') {
          agent {
            docker {
              image 'gradle:jdk11'
            }

          }
          steps {
            sh 'ci/build-app.sh'
            archiveArtifacts 'app/build/libs/'
            sh 'ls'
            deleteDir()
            sh 'ls'
            skipDefaultCheckout(true)
          }
        }

      }
    }

  }
}