	pipeline {
	    agent any 

	        stage('Functional Testing'){
	            steps {
	               echo "test"
			    git 'https://github.com/simitaws/Selenium-Course.git'
			    script {
				    sh(/mvn clean test/)
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
	

