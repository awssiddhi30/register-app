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
        stage('build image and push  to dockerhub'){
            steps {
               withCredentials([usernamePassword(credentialsId: 'dockerhub-access', usernameVariable: 'DOCKER_USER', passwordVariable: 'DOCKER_PASS')]) {
                 sh """
                    docker build -t siri30/registerapp:v11 .
                    echo "\$DOCKER_PASS" | docker login -u "\$DOCKER_USER" --password-stdin
                    docker push siri30/registerapp:v11
                    docker rmi siri30/registerapp:v11
                  """
                }
            }
 
           
        }
        stage('run docker image'){
            steps{
                sh "docker run -d --name SIGNINAPP -p 8080:8080 siri30/registerapp:v11"
            }

        }
    }
}
