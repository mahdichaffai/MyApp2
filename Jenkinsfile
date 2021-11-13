pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', 
                    branches: [[name: '*/main']],
                    extensions: [[$class: 'CloneOption', timeout: 120]],
                        userRemoteConfigs: [[
                            credentialsId: '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', 
                            url: 'https://github.com/mahdichaffai/MyApp2.git']]])
                }
            }
        }
        /*
        stage('Install') {
             steps{
                script{
                    sh "sudo npm install"
                }
            }
        }
        */
        stage('Build') {
             steps{
                script{
                    sh " ansible-playbook MyApp/ansible/build.yml -i MyApp/ansible/inventory/host.yml --private-key=/var/lib/jenkins/.ssh/id_rsa -u root"
                }
            }
        }
        
        stage('Docker'){
            steps{
                script{
                    sh "ansible-playbook MyApp/ansible/docker.yml -i MyApp/ansible/inventory/host.yml --private-key=/var/lib/jenkins/.ssh/id_rsa -u root"
                }
            }
        }
        
        }
        }
