pipeline {
    agent { label 'jenkins-agent' }
    tools {
        jdk 'java17'
        maven 'Maven3'
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