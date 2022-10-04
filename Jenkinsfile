pipeline {
  agent any
  stages {
    stage('Prebuild1') {
      steps {
	    sh 'npm install'
      }
    }
    stage('Unit test2') {
       steps {
	  sh 'npm run test-unit'
      } 
    }
    stage('Integration3') {
      when {
         anyOf {
            branch 'develop';
            branch 'main'
         }
      }
      steps {
	   sh 'npm run test-integration'
      }
    }
    stage('Delivery45') {
      when {
 	branch 'main'
      }
      steps {
        script {
          docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
            def im = docker.build("skandina/express-calculator")
            im.push()
          }
        }
      }
    }
  } 
}     

