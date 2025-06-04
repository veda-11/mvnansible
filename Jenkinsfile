pipeline {
    agent any  // Use any available agent
    environment {
        LANG = 'en_US.UTF-8'
        LC_ALL = 'en_US.UTF-8'
    } // Add this only if you get an error about UTF-8 encoding
    tools {
        maven 'Maven'  // Ensure this matches the Maven name configured in Jenkins
    }
    stages {
        stage('Checkout') {
            steps {
                git branch: 'master', url: 'https://github.com/guhanta/MAwebapp.git'
            }
        }
        stage('Build') {
            steps {
                sh 'mvn clean package'  // Run Maven build
            }
        }
        stage('Archive') {
            steps {
                archiveArtifacts artifacts: 'target/*.war', fingerprint: true
            }
        }
        stage('Deploy') {
            steps {
                sh 'mvn clean package'
                sh 'ansible-playbook ansible/playbook.yml -i ansible/hosts.ini'
            }
        }
    }
 }
 
