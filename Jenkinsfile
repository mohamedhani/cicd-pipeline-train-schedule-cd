pipeline {
    agent
      { node 
        {
          label 'devployment_server'
        }
      } 
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
              
                sh 'docker build .  -t mohamedhani/nodejs_project'    
                     
            }

        }
    
}
}
