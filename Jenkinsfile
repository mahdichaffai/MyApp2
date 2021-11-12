pipeline {
  agent any
    stages {
        stage('Pull') {
             steps{
                script{
                    checkout([$class: 'GitSCM', branches: [[name: '*/main']],
                        userRemoteConfigs: [[
                            credentialsId: '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', 
                            url: 'https://github.com/mahdichaffai/CD.git']]])
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
                    sh " ansible-playbook MyApp/ansible/build.yml -i MyApp/ansible/inventory/host.yml"
                }
            }
        }
        
        stage('Docker'){
            steps{
                script{
                    sh "ansible-playbook MyApp/ansible/docker.yml -i MyApp/ansible/inventory/host.yml"
                }
            }
        }
        
        }
        }
