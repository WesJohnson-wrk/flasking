pipeline {
  agent {
    node {
      label 'docker'
    }

  }
  stages {
    stage('Git') {
      parallel {
        stage('Git') {
          steps {
            git(url: 'https://github.com/WesJohnson-wrk/flask-jenkins', branch: 'main')
          }
        }
      }
    }
    
    stage('Stop container') {
      steps {
        sh 'sudo docker stop wesjohnsondoc/flask-jenkins-c'
      }
    }
    stage('Build Image') {
      steps {
        sh 'sudo docker image build -t wesjohnsondoc/flask-jenkins .'
      }
    }

    stage('Docker login') {
      steps {
        sh 'sudo docker login -u wesjohnsondoc -p dckr_pat_-t5dQyMVNe7BLiT6aGxXRAW--2k'
      }
    }

    stage('Docker push') {
      steps {
        sh 'sudo docker push wesjohnsondoc/flask-jenkins'
      }
    }
    stage('Docker run') {
      steps {
        sh 'sudo docker container run -d -p 5000:5000 --name flask-jenkins-c wesjohnsondoc/flask-jenkins'
      }
    }
  }
}
