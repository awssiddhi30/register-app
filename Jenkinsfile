pipeline{
    agent any
    tools{
        maven 'maven11'
        jdk 'java17'
    }
     parameters{
        string(name: 'IMAGE_TAG', description: 'Who should I say hello to?')
    }
    stages{
        stage('clean workspace'){
            steps{
                cleanWs()                
            }
        }
        stage('checkout from scm'){
            steps{
                git branch: 'main', credentialsId: 'git', url: 'https://github.com/awssiddhi30/register-app.git'
            }
        }
        stage('build application'){
            steps{
                sh "mvn clean package"
                
            }
            
        }
        stage('test application'){
            steps{
                sh "mvn test"
            }
        }
    }
}
