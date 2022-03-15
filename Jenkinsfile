pipeline {
  environment {
    PROJECT = "gj-playground"
    APP_NAME = "hipster-adservicetest_1"
    CLUSTER = "blibli-test"
    CLUSTER_ZONE = "us-central1-c"
    IMAGE_TAG = "gcr.io/gj-playground/adservice_test1"
  }
  agent {
    kubernetes {
      yaml """
apiVersion: v1
kind: Pod
metadata:
labels:
  component: ci
spec:
  containers:
  - name: gcloud
    image: gcr.io/google.com/cloudsdktool/cloud-sdk:latest
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
          sh "gcloud auth list"
          sh "PYTHONUNBUFFERED=1 gcloud builds submit --tag gcr.io/gj-playground/adservice_test1"
        }
      }
    }
  }
} 
