pipeline {
	agent any
	environment {
		IMAGE_NAME="caladreas/devoptics-frontend"
		IMAGE_TAG=""
	}
	stages {
		stage('Hello') {
			steps {
				println 'Hello World'
			}
		}
		stage('Build') {
			steps {
				script {
					IMAGE_TAG "${env.BUILD_ID}"
				}
			}
		}
		stage('Release') {
			environment{
				IMAGE_ID = "${IMAGE_NAME}:${IMAGE_TAG}"
			}
			steps {
				// Tell Deliver that this job produced the image ...
				gateProducesArtifact type: 'docker', id: "${IMAGE_ID}"
				// Trigger deploy job (downstream consumer)
				build job: 'devoptics/devoptics-release/master', imageId : "${IMAGE_ID}"
			}
		}
	}
}
