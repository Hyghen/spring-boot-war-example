pipeline {
  agent any
  tools {
        maven 'Maven' 
    }
  stages {
    stage('TEST') {
      steps {
        sh 'mvn test'
        echo 'testing is completed'
      }
    }
    stage('BUILD') {
      steps {
        sh 'mvn package'
        echo 'build completed'
      }
    }
    stage('DEPLOY TO TEST') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat9serverdetails', path: '', url: 'http://192.168.35.134:8080/')], contextPath: '/app', war: '**/*.war'
        echo 'deploying to testing server'
      }
    }
    stage('DEPLOY TO PROD') {
      steps {
        deploy adapters: [tomcat9(credentialsId: 'tomcat9serverdetails', path: '', url: 'http://192.168.35.128:8080/')], contextPath: '/app', war: '**/*.war'
        echo 'deploying to production server'
      }
    }
  }
  post {
    always {
      echo 'always run the build either failed or success'
    }
    failure {
      echo 'run when build is failed '
    }
    success {
      echo 'run when build is success'
    }
  }
}
