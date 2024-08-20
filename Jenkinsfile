#!groovy

pipeline { 
	agent none 
	environment {
        // Definir variables de entorno
        DOCKER_REGISTRY_URL = 'https://docker.io' // URL del registro Docker (Docker Hub)
        DOCKER_CREDENTIALS_ID = 'dockerhub_id' // ID de las credenciales en Jenkins
        IMAGE_NAME = 'my-image' // Nombre de la imagen Docker
        IMAGE_TAG = 'latest' // Etiqueta de la imagen Docker
    }
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
		stage('Maven package') { 
			agent { 
				docker { 
					image 'maven:3.5.0' 
				} 
			} 
			steps { 
				sh 'mvn clean package' 
			} 
		}
		stage('Docker Build') { 
			agent any 
			steps { 
				script {
					 // Autenticarse en el registro Docker
                    docker.withRegistry(DOCKER_REGISTRY_URL, DOCKER_CREDENTIALS_ID) {
						sh 'docker build -t grupo07/spring-petclinic:latest .' 
					}
				}
			} 
		} 
	} 
}