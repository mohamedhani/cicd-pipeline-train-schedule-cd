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
            when { brach 'master'}
            steps    
            {  
               sh echo "it is a stage"
               withCredentials([usernamePassword(credentialsId:'stage_web_server',usernameVariable :'USERNAME',passwordVariable:'PASSWORD')]) {
               sshPublisher
               (
                   continueOnError: false ,
                   failOnError: true ,
                   publisher:[
                    {
                        configName :'stage_server',
                        sshCredentials:{
                            username: "$USERNAME",
                            encryptedPassphrase: "$PASSWORD"
                        },
                        transfers:[
                            {
                                sourceFiles: 'dist/trainSchedule.zip', 
                                remoteDirectory: '/tmp/',
                                removePrefix :'dist/',
                                execCommand: 'sudo yum install unzip -y && sudo unzip /tmp/trainSchedule.zip && sudo mkdir /opt/cicd_project && sudo mv /tmp/trtrainSchedule/* /opt/cicd_project'
                           }]

                    }]
                )
            
            }   
        }
        }
    
}
}
