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
  - name: kaniko
    image: gcr.io/kaniko-project/executor:v1.0.0
    imagePullPolicy: Always
    volumeMounts:
      - name: docker-config
        mountPath: /kaniko/.docker
    resources:
      limits:
        cpu: 1
        memory: 1Gi
  volumes:
  - name: docker-config
    projected:
      sources:
      - secret:
          name: regcred
          items:
            - key: .dockerconfigjson
              path: config.json
"""
}
  }
  stages {
    stage ('SAST') {
      steps {
        container ('kaniko'){
          sh """
              /kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --destination=ravindra777/test
             """
        }
      }
    }
  } 
}


