node {
   stage('Preparation') { 
      git 'https://github.com/ktboopathi/fleetman-webapp'
   }
   stage('Build') {
      sh "mvn -DskipTests clean package"
   }
   stage('Results') {
      archive 'target/*.war'
   }
   stage('Deploy') {      
    withCredentials([aws(accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws-jenkins-user', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY')]) {
       ansiblePlaybook credentialsId: 'ssh-credentials', installation: 'ansible-installation', playbook: 'deploy.yaml'
    } 
  }   
}
