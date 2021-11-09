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
	        bat "docker rm -f jenkinscidev"
                bat "docker run --name jenkinscidev -itd -p 8082:8080 icatdocker/docker_jenkins_springboot:${BUILD_NUMBER} nginx ."
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
        stage(' Security Testing (SonarQube)'){
            steps {
	 git 'https://github.com/cwelland1/SpringbootJenkinsBuild.git'
	withSonarQubeEnv('SonarQube') {
		bat "mvn clean package sonar:sonar -Dsonar.login=cfb1a2c3b5624f88fc689d4027cb1e564f463039"
		sleep 5
		}
	    }
	}
       
        stage("Quality Gate (SonarQube)") {

          steps {
		  timeout(time: 3, unit: 'MINUTES') {
             waitForQualityGate abortPipeline: true

                }
	  }
                
            }
        
        stage('Deploy to UAT  (Docker)'){
            steps {
             echo "UAT Deployment in Progress"
//		bat "mvn package"
//                bat "docker build -t  icatdocker/docker_jenkins_springboot:${BUILD_NUMBER} ."
//                  withCredentials([string(credentialsId: 'Dockerid', variable: 'Dockerpwd')]) {
//                bat "docker login -u icatdocker -p ${Dockerpwd}"
//                bat "docker push icatdocker/docker_jenkins_springboot:${BUILD_NUMBER}"
	        bat "docker rm -f jenkinsciuat"
                bat "docker run --name jenkinsciuat -itd -p 8083:8080 icatdocker/docker_jenkins_springboot:${BUILD_NUMBER} nginx ."
//            }
            }
        }

	 stage('Deploy to Prod  (Docker)'){
            steps {
             echo "Prod Deployment in Progress"
//		bat "mvn package"
//                bat "docker build -t  icatdocker/docker_jenkins_springboot:${BUILD_NUMBER} ."
//                  withCredentials([string(credentialsId: 'Dockerid', variable: 'Dockerpwd')]) {
//                bat "docker login -u icatdocker -p ${Dockerpwd}"
//                bat "docker push icatdocker/docker_jenkins_springboot:${BUILD_NUMBER}"
	        bat "docker rm -f jenkinsciprod"
                bat "docker run --name jenkinsciprod -itd -p 8083:8080 icatdocker/docker_jenkins_springboot:${BUILD_NUMBER} nginx ."
//            }
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
