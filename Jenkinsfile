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

	  withCredentials([string(credentialsId: 'kubeconfig-credential-id', variable: 'KUBECONFIG_CONTENT')]) {
                    sh '''
                        echo "$KUBECONFIG_CONTENT" > kubeconfig.yaml
			cat kubeconfig.yaml
                        export KUBECONFIG=$(pwd)/kubeconfig.yaml
			cat KUBECONFIG

                        helm upgrade --install --force vprofile-stack helm/vprofilecharts --set appimage=${registry}:V31 -n test
                    '''
            steps {
            }
        }
    }
}
