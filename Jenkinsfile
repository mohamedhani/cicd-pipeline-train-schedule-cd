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
        stage ('build docker image'){
            when { branch 'master'}
            steps    
            {  
              sh "docker build . -t node_project"
              sh "docker push mohamedhani/node/project"
                     
            }

        }
    
}
}
