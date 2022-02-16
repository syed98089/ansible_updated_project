pipeline {
    agent any
       tools{
           maven "Maven"
              }
    stages {
        stage('Checkout') {
            steps {
              
              checkout([$class: 'GitSCM', branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[credentialsId: 'github_code_pull', url: 'https://github.com/syed98089/ansible_project_updated.git']]]) 
                }
                }
             

         stage('Build for package artifact') {
            steps {
                sh 'mvn clean package'
                }
               }
         stage('Ansible-playbook-executing') {
            steps {
              ansiblePlaybook credentialsId: 'ansible-key', disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: '/home/ansible/playbook/myplaybook.yml'
                  
               }
               }

}
}
