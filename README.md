# CI-CD-Jenkins-ArgroCD

### Jenkins plugins

Install the following plugins in Jenkins for the demo.

- Docker plugin
- Docker Pipeline plugin
- GitHub Integration Plugin
- Parameterized trigger Plugin

### ArgoCD installation

Install ArgoCD in your Kubernetes cluster following this link - https://argo-cd.readthedocs.io/en/stable/getting_started/

### To Start

- Edit Jenkinsfile - part of "stage('Build image')"
- Create docker hub repository
- Install Jenkins
- Install Jenkins Plugin
- Create Access Token on github
- Register github credentials on Jenkins
- Register dockerhub credentials on Jenkins
- Create Item on Jenkins for Docker Pipeline
- Create Pipeline on Jenkins for Kube Pipeline
- Install Argo CD
- Setup Argo CD
- Set Webhooks on Github
- create new commit to test

### Continue

- https://github.com/feelgoodsoo/CICD-yaml-for-kube
