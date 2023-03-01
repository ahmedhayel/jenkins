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
        sh 'mvn clean install'
      }
    }

    stage('Test Step') {
      parallel {
        stage('Test Step') {
          steps {
            sh 'mvn test'
          }
        }

        stage('Sonar analysis Step') {
          steps {
            sh 'mvn verify sonar:sonar -Dsonar.projectKey=io.ecommerce:basic-ecommerce -Dsonar.host.url=http://localhost:9000 -Dsonar.login=sqp_211cca4cc632ba8f6b7c20861559297168612d2d'
          }
        }

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
}