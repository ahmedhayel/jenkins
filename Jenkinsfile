pipeline {
  agent any
  stages {
    stage('Checkout Step') {
      steps {
        git(url: 'https://github.com/ahmedhayel/basic-ecommerce.git', branch: 'master', credentialsId: 'token-for-private-repo')
      }
    }

    stage('Build Step') {
      steps {
        sh 'mvn clean package'
      }
    }

    stage('Test Step') {
      steps {
        sh 'mvn test'
      }
    }

    stage('Build Image') {
      steps {
        sh 'docker build -t ecommerce-app .'
      }
    }

    stage('Deploy to dockerhub') {
      steps {
        sh 'docker login -u ahmedhayel -p _Ahmed#hayel123@_'
        sh 'docker push ahmedhayel/ecommerce-app'
      }
    }

  }
  tools {
    maven 'maven-3.6.3'
  }
}