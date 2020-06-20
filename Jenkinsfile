pipeline {
    agent any
    stages {
        stage('Build') {
            steps {
                echo 'Running build automation'
                sh './gradlew build --no-daemon'
                archiveArtifacts artifacts: 'dist/trainSchedule.zip'
            }
        }
        stage ('deploy on stage '){
            when { branch 'master'}
            steps    
            {  
                echo "it is a stage"
               withCredentials([usernamePassword(credentialsId:'stage_web_server',usernameVariable :'USERNAME',passwordVariable:'PASSWORD')]) {
              sshPublisher(
                  publishers:[sshPublisherDesc (
                    configName: 'stage_server',
                    sshCredentials: [
                    encryptedPassphrase: "mohamed", 
                    username: "mohamed"
                     ],
                transfers: [sshTransfer(
                    sourceFiles: 'dist/trainSchedule.zip',
                    removePrefix: 'dist/', 
                     remoteDirectory: '/opt',
                     execCommand: ' sudo yum install unzip -y && sudo unzip /tmp/trainSchedule.zip && sudo mkdir /opt/cicd_project && sudo mv /tmp/trtrainSchedule/* /opt/cicd_project'
                         )],
                       )])
            
            }   
        }
        }
    
}
}
