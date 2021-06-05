node{
  stage('SCM Checkout'){
   git credentialsId: 'gituhb-cred', url: 'https://github.com/MeVsMe-cloud/sampleApplication'
  }
  stage('Build Docker Image'){
   sh 'docker build -t dockerjenkins444/mysecondrepo:1.0.0 .'
  }
  stage('Push Docker Image'){
    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerHubPwd')]) {
      sh "docker login -u dockerjenkins444 -p ${dockerHubPwd}" 
  }
   sh 'docker push dockerjenkins444/mysecondrepo:1.0.0'
  }
}
