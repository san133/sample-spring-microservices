pipeline {
agent {
label 'worker-node'
}

stages {

stage ('Checkout') 
{
steps
    {
    
        checkout scm
        
    }
    
}
stage ('Build') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/account-service/account-service ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/account-service/account-service ; sudo docker build -t account-service . " 
    }
}
     stage ('dockerimagepush') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/account-service/account-service ; sudo  docker login -usand3cs -pMrvsa@123 "
        sh "cd /home/ubuntu/workspace/account-service/account-service ; sudo docker tag account-service sand3cs/account-service "
        sh "cd /home/ubuntu/workspace/account-service/account-service ; sudo docker push sand3cs/account-service  "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node ( ' ansible-server '  ) {
             sh " sudo ansible-playbook /root/k8s.yaml"
   
    }
}
}
}
    
    
}
