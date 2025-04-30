pipeline {

    agent any

	tools {
        maven "MAVEN3"
    }

    environment {
        registry = "kofipat/vprofileapp"
        registryCredential = 'dockerhub'

	KUBECONFIG = credentials('kubeconfig-credential-id')
    }

    stages{
        stage('Kubernetes Deploy') {
          agent {label 'BAK'}
            steps {
              sh "helm upgrade --install --force vprofile-stack helm/vprofilecharts --set appimage=${registry}:V31 -n test"
            }
        }
    }
}
