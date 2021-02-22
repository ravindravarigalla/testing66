pipeline {

  environment {
    PROJECT = "halodoc-fisclouds"
    APP_NAME = "lazarus"
    FE_SVC_NAME = "${APP_NAME}"
    CLUSTER = "gke-cicd"
    CLUSTER_ZONE = "us-central1-c"
    IMAGE_TAG = "us.gcr.io/${PROJECT}/${APP_NAME}:latest"
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
  - name: gcloud
    image: gcr.io/google.com/cloudsdktool/cloud-sdk:latest
    command:
    - cat
    tty: true
  - name: helm
    image: gcr.io/dazzling-scheme-281712/helm3-test 
    command:
    - cat
    tty: true
"""    
}
  }
  stages {
    stage('Build and push image with Container Builder') {
      steps {
        container('gcloud') {
          sh "PYTHONUNBUFFERED=1 gcloud builds submit -t gcr.io/dazzling-scheme-281712/sampleapp ."
  
        }
      } 
    }
  stage('Deploy ') {
      steps {
        container('helm') {
          sh """
          gcloud container clusters get-credentials cluster-1 --zone us-central1-c --project dazzling-scheme-281712
          helm install sampleapp sampleapp -n default 
          """ 
        }
      }
    }
   }
 }
