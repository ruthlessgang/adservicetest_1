pipeline {
  environment {
    PROJECT = "gj-playground"
    CLUSTER = "cluster-1"
    CLUSTER_ZONE = "us-central1-c"
    IMAGE_TAG = "gcr.io/gj-playground/adservicenew"
    JENKINS_CRED = "gj-playground"
  }
  agent {
    kubernetes {
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  name: kaniko
labels:
  component: ci
spec:
  restartPolicy: Never
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
    stage('Bake') {
      steps {
        container('kaniko') {
            sh '''
            sh "gcloud auth list"
            sh "PYTHONUNBUFFERED=1 gcloud builds submit -t  gcr.io/gj-playground/adservice . "
            '''
        }
      }
      
      }
    }
}
