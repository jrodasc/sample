pipeline {
  agent {
    docker {
      image 'node:6-alpine'
      args '-p 3002:3000'
    }

  }
  stages {
    stage('Install') {
      steps {
        sh 'npm install'
      }
    }
    stage('Build') {
      steps {
        sh 'npm run build'
      }
    }
    stage('Test') {
      steps {
        sh 'npm test'
        emailext(subject: 'Aprobar', body: 'Por favor aprueba', attachLog: true)
      }
    }
    stage('Approve') {
      when {
           branch 'production'
      }
      steps {
        input(message: '¿Se aprueba?', submitter: 'dev2')
      }
    }
    stage('Deploy to development') {
      when {
         branch 'develoment' 
      }
      steps {
        echo 'Succesful'
      }
    }
    stage('Deploy to production') {
      when {
         branch 'production' 
      }
      steps {
        echo 'Succesful'
      }
    }
  }
}
