pipeline {
    agent { label 'jenkins-agent' }
    tools {
        java 'java17'
        maven 'maven3'
    }
    stages {
        stage("clear workspace") {
            steps {
                clearWs()
            }
        }
        stage("checkout from SCM") {
            steps {
                git branch: 'main' , credentialsId: 'github' , url: 'https://github.com/kishorethakur1998/register-app.git'
            }
        }
        stage("Build Application") {
            steps {
                sh 'mvn clear package'
            }
        }
        stage("Test Application") {
            steps {
                sh 'mvn test'
            }
        }
    }
}