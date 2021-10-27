pipeline {
    agent any 
    stages {
        stage('Compile and Build  (Maven)') { 
            steps {
                bat "mvn clean compile"
            }
        }
       

        stage('Deploy to Dev   (Docker)') { 
            steps {
                bat "mvn package"
                bat "docker build -t  icatdocker/docker_jenkins_springboot:${BUILD_NUMBER} ."
                  withCredentials([string(credentialsId: 'Dockerid', variable: 'Dockerpwd')]) {
                bat "docker login -u icatdocker -p ${Dockerpwd}"
                bat "docker push icatdocker/docker_jenkins_springboot:${BUILD_NUMBER}"
	        bat "docker rm -f jenkinsci"
                bat "docker run --name jenkinsci -itd -p  141.156.161.26:8081:8080 icatdocker/docker_jenkins_springboot:${BUILD_NUMBER} ."
            }
        }
    }

 	 stage('Functional Testing   (Selenium)'){
	  steps {
	         echo "test"
                 git 'https://github.com/simitaws/Selenium-Course.git'
	         script {
		        bat(/mvn clean test/)
			    }
	            }
	        }

           stage(' Security Testing  (SonarQube)'){
            steps {
                echo "test"
                sleep 5
            }
        }
        
        stage('Deploy to UAT  (Docker)'){
            steps {
             echo "test"
            }
        }

        
        stage('Archiving') { 
            steps {
//                 archiveArtifacts '**/target/*.jar'
		    sleep 2
            }
        }
    }
}
