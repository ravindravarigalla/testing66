pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                sh """
                   docker images
                   docker build -t test .
                   docker tag test ravindra777/adservice:v2
                   docker login -u ravindra777 -p ravindra77
                   docker push ravindra777/adservice:v2
                   """
            }
        }
    }
}
