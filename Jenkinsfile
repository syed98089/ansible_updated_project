pipeline {
    agent any
       tools{
           maven "Maven"
              }
    stages {
        stage('Checkout') {
            steps {
              checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_code_pull', url: 'https://github.com/syed98089/new_repo.git']]])
                }
                }
             

         stage('Build for package artifact') {
            steps {
                sh 'mvn clean package'
                }
               }
        
         stage('After Build code transfer to ansible server') {
            steps {
                       sshagent(['ansiblekey']) {
                      sh "scp -o StrictHostKeyChecking=no /var/lib/jenkins/workspace/job1/webapp/target/webapp.war ec2-user@175.41.157.55:/opt"
                           
                         
                       }
                }
               }
         stage('Ansible-playbook-executing') {
            steps {
              ansiblePlaybook credentialsId: 'ansiblekey', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: '/opt/playbook'
               }
               }



}
}
