pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        echo 'Esto es un mensaje'
      }
    }
    stage('Test') {
      parallel {
        stage('DBUnit') {
          steps {
            timeout(time: 10, unit: 'MINUTES') {
              echo 'a'
            }

            retry(count: 10) {
              echo '1..'
            }

          }
        }
        stage('JUnit') {
          steps {
            sleep 5
            bat 'mkdir hola'
          }
        }
        stage('Jasmine') {
          steps {
            archiveArtifacts 'Storage'
          }
        }
      }
    }
    stage('Browser Test') {
      parallel {
        stage('FireFox') {
          steps {
            acceptGitLabMR(mergeCommitMessage: 'Merge Commit Message')
            addGitLabMRComment(comment: 'Coment 1')
          }
        }
        stage('Edge') {
          steps {
            ws(dir: 'Pipeline2') {
              echo 'c'
            }

          }
        }
        stage('Safari') {
          steps {
            sleep 5
          }
        }
        stage('Chrome') {
          steps {
            build 'BuildSample'
          }
        }
      }
    }
    stage('Dev') {
      steps {
        isUnix()
        pwd(tmp: true)
      }
    }
    stage('Production') {
      steps {
        sleep 15
      }
    }
  }
}