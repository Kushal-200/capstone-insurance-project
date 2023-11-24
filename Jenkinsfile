node{
    stage('code checkout'){
        git 'https://github.com/Kushal-200/capstone-insurance-project.git'
    }

    
    stage('build'){
      sh 'mvn clean package'  
    }
    
    stage('package as docker image'){
      sh 'docker build -t Kushal-200/capstone-insurance-project:1.0 .'
    }
    
    stage('push to dockerhub'){
        
    withCredentials([string(credentialsId: 'DockerPass', variable: 'DockerPass')]) {
    sh "docker login -u Kushal-200 -p ${DockerPass}"
    sh 'docker push Kushal-200/capston-insurance-project:1.0'
    }
    }
    
    stage('deploy to test-environment') {
        ansiblePlaybook become: true,  disableHostKeyChecking: true, installation: 'ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server.yml'
    }
    
    
    
}
