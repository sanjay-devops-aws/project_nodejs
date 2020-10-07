pipeline{
    agent any
    
    stage('GIT CHECKOUT')
    {
       git credentialsId: 'cbc24122-81d4-4adc-84a9-dc471ca3bfeb', url: 'https://github.com/sanjay-devops-aws/project_nodejs.git'
    }
		
    
    stage('DOCKER BUILD')
    {
        sh 'docker build -t sanju/node:1.0 .'
    }
    
    stage('PUSH TO DOCKERHUB')
    {
       withDockerRegistry(credentialsId: '52cf0393-f2c5-415b-8e6a-0020a69dc588', url: 'https://index.docker.io/v1/') {
             sh 'docker push sanju/node:1.0'  
       }
    }
    
     
    stage('PULL FROM DOCKERHUB')
    {
       withDockerRegistry(credentialsId: '52cf0393-f2c5-415b-8e6a-0020a69dc588', url: 'https://index.docker.io/v1/') {
             sh 'docker pull sanju/node:1.0'  
       }
    }
    
    stage('DEPLOY IN KUBERNETES')
    {
      dir('/var/lib/jenkins/workspace/node')
      {
         sh 'kubectl apply -f Deployment.yml'
      }
    }
    
}
