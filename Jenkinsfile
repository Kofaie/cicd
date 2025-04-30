pipeline {

    agent any

	tools {
        maven "MAVEN3"
    }

    environment {
        registry = "kofipat/vprofileapp"
        registryCredential = 'dockerhub'
    }

    stages{
        stage('Kubernetes Deploy') {
          agent {label 'BAK'}
		steps {
			withCredentials([string(credentialsId: 'kubeconfig-credential-id', variable: 'kubeconfig-credential-id')]) {
                    		sh '''
                        	echo "$kubeconfig-credential-id" > kubeconfig.yaml
				export KUBECONFIG=$(pwd)/kubeconfig.yaml
				cat ~/.kube/config

                        	helm upgrade --install --force vprofile-stack helm/vprofilecharts --set appimage=${registry}:V31 -n test
                    		'''
			}
        		}
    		}
	}
}
