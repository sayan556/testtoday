def remote = [:]
remote.name = 'test'
remote.host = '54.177.240.166'
remote.port = 22
remote.allowAnyHosts = true


pipeline {
agent any

   stages {
     stage('git clone') {
       steps {
           git branch: 'main', credentialsId: 'githubcred', url: 'https://github.com/sayan556/testtoday.git'
         }
       }
     stage('deployment') {
       steps {
          script {
           withCredentials([usernamePassword(credentialsId: 'sayanID', passwordVariable: 'password', usernameVariable: 'username')]) {
    // some block

               remote.user = "$username"
               remote.password = "$password"
               sshPut remote : remote, from: "deployment.yaml" , into: "/home/sayan"
               sshCommand remote: remote, command: "kubectl apply -f deployment.yaml"

            }
          }
        }
     }
   }

}
