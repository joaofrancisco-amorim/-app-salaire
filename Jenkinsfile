node{
      stage('Clone') {
          checkout scm
      }
      stage('SSH') {
        sh "apk add ansible sshpass"
        sh "rm -rf /root/.ssh"
        sh "echo \"172.28.141.126 app-salaire.corentin.form\" > /etc/hosts"
        sh "ssh-keygen -q -t rsa -N '' -f ~/.ssh/id_rsa"
        sh "sshpass -p 'root' ssh-copy-id -o stricthostkeychecking=no root@172.28.141.126"
      }
      stage('Ansible') {
        ansiblePlaybook (
            inventory: 'hosts.yaml',
            playbook: 'playbook.yaml',
            colorized: true,
        )
      }
}
