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
       sh "cd /home/ubuntu/workspace/project/customer-service ; mvn clean install " 
    }
}

   
stage ('dockerimageBuild')
    {
    steps
    {
        sh "cd /home/ubuntu/workspace/project/customer-service ; sudo docker build -t customer-service . " 
    }
}
     stage ('dockerimagepush ') 
{
    steps
    {
       sh "cd /home/ubuntu/workspace/project/customer-service ; sudo  docker login -usand3cs -psandeep1234 "
        sh "cd /home/ubuntu/workspace/project/customer-service ; sudo docker tag customer-service sand3cs/customer-service "
        sh "cd /home/ubuntu/workspace/project/customer-service ; sudo docker push sand3cs/customer-service  "
        
        
    }
}
    
    
stage ('k8sdeployment') 
    {
        steps {
            node ( ' ansible-server' ) {
             sh " sudo ansible-playbook /root/k8s.yaml"
   
    }
}
}
}
    
    
}
