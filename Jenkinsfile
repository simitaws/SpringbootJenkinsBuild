pipeline {
    agent any 
    stages {
        stage('Compile and Build') { 
            steps {
                bat "mvn clean compile"
            }
        }
       

        stage('Deploy to Dev') { 
            steps {
                bat "mvn package"
                bat "docker build -t  icatdocker/docker_jenkins_springboot:${BUILD_NUMBER} ."
                  withCredentials([string(credentialsId: 'Dockerid', variable: 'Dockerpwd')]) {
                bat "docker login -u icatdocker -p ${Dockerpwd}"
                bat 'docker push icatdocker/docker_jenkins_springboot:${BUILD_NUMBER}'
                bat 'docker rm -f $(docker ps -a -q)'
                bat 'docker run -itd -p  8081:8080 icatdocker/docker_jenkins_springboot:${BUILD_NUMBER}'
            }
        }
    }

 	 stage('Functional Testing'){
	  steps {
	         echo "test"
                 git 'https://github.com/simitaws/Selenium-Course.git'
	         script {
		        bat(/mvn clean test/)
			    }
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
