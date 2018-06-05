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
            catchError() {
              sh '''time
echo "Es la hora de la diversión"'''
            }

          }
        }
      }
    }
    stage('Dev') {
      steps {
        isUnix()
        pwd(tmp: true)
        input(message: 'Que te ha parecido?', id: '1,2,3', ok: '1,2,3')
      }
    }
    stage('Staging') {
      steps {
        emailext(subject: 'Envío de correo', body: 'Este es un envio de correo de prueba lanzado desde el plugin de Jenkins BlueOcean. Alguien me oye¿', to: 'alsanchez@inlogiq.com')
      }
    }
    stage('Production') {
      steps {
        input(message: 'Introduzca un numero', ok: '1', id: '1')
        sleep 15
      }
    }
  }
}