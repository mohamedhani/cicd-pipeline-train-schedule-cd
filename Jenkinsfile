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
                     remoteDirectory: '/home/mohamed',
                         )],
                       )])
            
            }   
        }
        }
    
}
}
