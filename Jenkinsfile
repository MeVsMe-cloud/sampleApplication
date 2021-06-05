node{
  stage('SCM Checkout'){
   git credentialsId: 'gituhb-cred', url: 'https://github.com/MeVsMe-cloud/sampleApplication'
  }
  stage('MVN packaging'){
    def MAVEN_HOME = tool name: 'maven-3', type: 'maven'
    def mvnCMD = "${MAVEN_HOME}/bin/mvn"
    sh "${mvnCMD} clean package" 
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
   stage('Deployment in Dev Environment'){
     def dockerRun = 'docker run -p 8080:8080 -d --name mySampleApp dockerjenkins444/mysecondrepo:1.0.0'
     sshagent(['dev-server']) {
       sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.58.121 ${dockerRun}"
   }
  }
}
