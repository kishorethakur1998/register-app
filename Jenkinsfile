pipeline {
    agent { label 'jenkins-agent' }
    tools {
        jdk 'java17'
        maven 'Maven3'
    }
    stages {
        stage("clear workspace") {
            steps {
                cleanWs()
            }
        }
        stage("checkout from SCM") {
            steps {
                git branch: 'main' , credentialsId: 'github' , url: 'https://github.com/kishorethakur1998/register-app.git'
            }
        }
        stage("Build Application") {
            steps {
                sh 'mvn clean package'
            }
        }
        stage("Test Application") {
            steps {
                sh 'mvn test'
            }
        }
        stage("sonarqube analysis") {
            steps {
                script {
                    withSonarQubeEnv(credentialsId: 'jenkins-sonarqube-token') {
                    sh "mvn sonar:sonar"
                    }
                }    
            }
        }
        stage ("Quality gates") {
            steps {
                script {
                    waitForQualityGate abortPipeline: false, credentialsId: "jenkins-sonarqube-token"
                }
            }
        }
    }
}