pipeline{
    agent any 
    environment {
        PATH = "$PATH:/opt/maven/bin"
    }
    stages{
       stage('GetCode'){
            steps{
                git 'https://github.com/vikramDevPrac/java-login-app.git'
            }
         }
       stage('Build') {
      steps {
        sh '"mvn" -Dmaven.test.failure.ignore clean install'
      	}
    	}
	stage('Test'){
		steps{
                sh 'mvn test'
                 }
            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                }
            }
         }
	 stage('Build image') {
		 steps {
        /* This builds the actual image; synonymous to
         * docker build on the command line */

        	docker.build("getintodevops/hellonode")
		 }
    }
        
	//stage('Deploy') {
      //steps {   
      //   deploy adapters: [tomcat8(credentialsId: 'deploy', path: '', url: 'http://3.110.134.168:8080')], contextPath: null, war: '**/**.war'
      //}
    //}
       
    }
}
