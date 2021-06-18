def remote = [:]
remote.name = 'test'
remote.host = '192.168.1.105'
remote.port = 22
remote.allowAnyHosts = true


pipeline {
agent any

   stages {
     stage('git clone') {
       steps {
           git branch: 'main', credentialsId: 'githubcred', url: 'https://github.com/sayan556/ec2test.git'
         }
       }
     stage('deployment') {
       steps {
          script {
           withCredentials([usernamePassword(credentialsId: 'sshcredential', passwordVariable: 'password', usernameVariable: 'username')]) {
    // some block

               remote.user = username
               remote.password = password
               sshPut remote : remote, from: "index.html" , into: "/var/www/html"
            }
          }
        }
     }
   }

}
