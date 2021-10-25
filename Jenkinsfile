	pipeline {
	    agent any 
		stages {
	stage('build') {
      cmd_exec('echo "Buils starting..."')
}

def cmd_exec(command) {
    return bat(returnStdout: true, script: "${command}").trim()
}
	        stage('Functional Testing'){
	            steps {
	               echo "test"
			    git 'https://github.com/simitaws/Selenium-Course.git'
			    script {
				    bat(/mvn clean test/)
			    }
	                sleep 4
	            }
	        }
	

	           stage(' Security Testing'){
	            steps {
	                echo "test"
	                sleep 5
	            }
	        }
	        
	        stage('Deploy to UAT'){
	            steps {
	             echo "test"
	            }
	        }
	

	        
	        stage('Archving') { 
	            steps {
	                 archiveArtifacts '**/target/*.jar'
	            }
	        }
	    }
	}
