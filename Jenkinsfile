#!groovy

pipeline { 
	agent none 
	stages { 
		stage('Maven Install') { 
			agent { 
				docker { 
					image 'maven:3.5.0' 
				} 
			} 
			steps { 
				sh 'mvn clean install' 
			} 
		} 
		stage('Docker Build') { 
			agent any 
			steps { 
				withCredentials([usernamePassword(credentialsId: DOCKER_CREDENTIALS_ID, usernameVariable: 'fpogo', passwordVariable: '7Mpuc9kb')]) {
                        sh '''
							echo $DOCKER_PASSWORD | docker login -u $DOCKER_USERNAME --password-stdin
                            docker images
						'''
                }
				sh 'docker build -t grupo07/spring-petclinic:latest .' 
			} 
		} 
	} 
}