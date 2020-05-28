pipeline {
	agent any
	environment {
		IMAGE_NAME="caladreas/devoptics-frontend"
	}
	stages {
		stage('Build') {
			steps {
				println 'building docker image, I swear...'
			}
		}
		stage('Release') {
			environment{
				IMAGE_ID = "${IMAGE_NAME}:${env.BUILD_ID}"
			}
			steps {
				// Tell Deliver that this job produced the image ...
				gateProducesArtifact type: 'docker', id: "${IMAGE_ID}"
				// Trigger deploy job (downstream consumer)
				build job: 'devoptics/devoptics-release/master', parameters: [string(name: 'FRONTEND_IMAGE_ID', value: "${IMAGE_ID}")]
			}
		}
	}
}
