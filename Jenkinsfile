pipeline {
    agent
      { node 
        {
          label 'k8s_deployment'
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
                sh 'docker build .  -t localregistry:5000/nodejs'  
                sh 'docker push localregistry:5000/nodejs'    
            }

        }
      stage ('k8s deployment') 
      {   when { branch 'master' }
          steps 
         {
             sh 'kubectl apply -f k8s_project.yaml'
         }
      } 

       
    
}
}
