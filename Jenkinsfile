node{
    stage('code checkout'){
        echo 'checking repo code cloned'
        git 'https://github.com/harshpgoti/insure-me.git'
    }
    
    stage('configure test-server and deploy insure-me'){
        echo "configuring test-server"
        ansiblePlaybook become: true, credentialsId: 'ssh-key', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-prod-server.yml'
    }
    
    stage('selenium script clone'){
        echo 'cloning the selenium script'
        sh 'cd ..'
        sh 'mkdir -p insure-me-selenium-script'
        git 'https://github.com/harshpgoti/insure-me-selenium-script.git'
        sh 'cd insure-me-selenium-script'
    }
    
    stage('run insure-me-selenium-script'){
        echo "run insure-me-selenium-script"
        ansiblePlaybook become: true, credentialsId: 'ssh-key', disableHostKeyChecking: true, installation: 'Ansible', inventory: '/etc/ansible/hosts', playbook: 'configure-test-server-selenium-script.yml'
    }
}