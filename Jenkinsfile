node{
  stage('SCM Checkout'){
   git credentialsId: 'gituhb-cred', url: 'https://github.com/MeVsMe-cloud/sampleApplication'
  }
  stage('Build Docker Image'){
   sh 'sudo docker build -t dockerjenkins444/mysecondrepo:1.0.0 .'
  }
  stage('Push Docker Image'){
    withCredentials([string(credentialsId: 'dockerhub-pwd', variable: 'dockerHubPwd')]) {
      sh "sudo docker login -u dockerjenkins444 -p ${dockerHubPwd}" 
  }
   sh 'sudo docker push dockerjenkins444/mysecondrepo:1.0.0'
  }
   stage('Deployment in EKS Cluster'){
     kubernetesDeploy configs: '*.yaml', dockerCredentials: [[credentialsId: 'docker-cred-for-k8s']], kubeConfig: [path: ''],
       kubeconfigId: 'k8s', secretName: '', ssh: [sshCredentialsId: '*', sshServer: 'ec2-user@172.31.22.228'],
       textCredentials: [certificateAuthorityData: '', clientCertificateData: '', clientKeyData: '',
                         serverUrl: 'https://DBF1883A889B1C56F313FE09A48DF40C.yl4.us-east-1.eks.amazonaws.com']
  }
 }
