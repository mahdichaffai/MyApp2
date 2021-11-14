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
                    sh " ansible-playbook ansible/build.yml -i ansible/inventory/host.yml --private-key=/var/lib/jenkins/.ssh/id_rsa -u root"
                }
            }
        }
        
        stage('Docker'){
            steps{
                script{
                    sh "ansible-playbook ansible/docker.yml -i ansible/inventory/host.yml --private-key=/var/lib/jenkins/.ssh/id_rsa -u root"
                }
            }
        }
        
        stage('dockerHub') {
             steps{
                script{
                    sh "ansible-playbook ansible/registry.yml -i ansible/inventory/host.yml --private-key=/var/lib/jenkins/.ssh/id_rsa -u root"
                }
            }
        }
        
        }
        }
    
    
