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
  - name: sonar-scanner
    image: sonarsource/sonar-scanner-cli
    command:
    - cat
    tty: true
"""
}
  }
  stages {
    stage ('SAST') {
      steps {
        container ('sonar-scanner'){
          sh """
              sonar-scanner \
               -Dsonar.projectKey=cartservice \
               -Dsonar.sources=. \
               -Dsonar.host.url=http://34.67.53.8:9000 \
               -Dsonar.login=b7d5646b95b8e022db198431a949d8766ff82f0d
             """
        }
      }
    }
  } 
}


