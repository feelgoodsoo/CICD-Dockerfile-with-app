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
    volumeMounts:
    - name: kaniko-secret
      mountPath: /kaniko/.docker
  volumes:
  - name: kaniko-secret
    secret:
      secretName: regcred-pilsu
      items:
        - key: .dockerconfigjson
          path: config.json
'''
        }
    }
    stages {
       stage('Checkout') {
          steps {
            container('kaniko') {
              git branch: 'main', url: 'https://github.com/feelgoodsoo/CICD-Dockerfile-with-app.git'
            }
          }
        }
        stage('Build & Tag & Push Docker Image') {
            steps {
                container('kaniko') {
                    sh "/kaniko/executor --dockerfile `pwd`/Dockerfile --context `pwd` --destination=pilsu/cicd:$BUILD_NUMBER"
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
