pipeline {
  environment {
    PROJECT = "gj-playground"
    CLUSTER = "test"
    CLUSTER_ZONE = "us-central1-c"
    IMAGE_TAG = "gcr.io/gj-playground/adservice"
    JENKINS_CRED = "gj-playground"
  }
  agent {
    kubernetes {
      defaultContainer 'jnlp'
      yaml """
apiVersion: v1
kind: Pod
metadata:
  name: sample
labels:
  component: ci
spec:
  restartPolicy: Never
  containers:
  - name: gcloud
    image: gcr.io/google.com/cloudsdktool/cloud-sdk:slim
    command:
    - cat
    tty: true
  
  """
}
  }
  stages {
    stage('Bake') {
      steps {
        container('gcloud') {
            sh '''
            sh "gcloud auth list"
            sh "PYTHONUNBUFFERED=1 gcloud builds submit -t  gcr.io/gj-playground/adservice . "
            '''
        }
      }
      
      }
    }
}
