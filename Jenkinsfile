pipeline {
  environment {
    PROJECT = "adira-playground"
    APP_NAME = "hipster-cartservice"
    CLUSTER = "gke-cluster-public"
    CLUSTER_ZONE = "asia-southeast1-a"
    IMAGE_TAG = "gcr.io/${PROJECT}/${APP_NAME}"
    JENKINS_CRED = "${PROJECT}"
  }
  agent {
    kubernetes {
      
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  # Use service account that can deploy to all namespaces
  containers:
  - name: helm
    image: gcr.io/dazzling-scheme-281712/helm3-test
    command:
    - cat
    tty: true
"""
}
  }
  stages {
    stage ('SAST') {
      steps {
        container ('helm'){
          sh """
              kubectl get pods -n bootcamp
             """
        }
      }
    }
  } 
}


