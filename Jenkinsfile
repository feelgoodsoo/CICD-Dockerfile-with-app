pipeline {
    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: kaniko
    image: gcr.io/kaniko-project/executor:debug
    command:
    - sleep
    args:
    - infinity
'''
        }
    }
    stages {
        stage('Build & Tag & Push Docker Image') {
            steps {
                container('kaniko') {
                    sh "executor --context=dir:///home/jenkins/agent/workspace/ --destination=pilsu/cicd:$BUILD_NUMBER --destination=pilsu/cicd:latest"
                }
            }
        }
        stage('Trigger ManifestUpdate') {
            steps {
                script {
                    echo "triggering updatemanifestjob"
                    build job: 'updatemanifest', parameters: [string(name: 'DOCKERTAG', value: env.BUILD_NUMBER)]
                }
            }
        }
    }
}
