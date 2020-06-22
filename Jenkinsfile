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
               withCredentials([usernamePassword(credentialsId: 'dockerhub', passwordVariable: 'PASSWORD', usernameVariable: 'USERNAME')]) {
                   sh 'docker login -u $USERNAME -p $PASSWORD'
                }  
                sh 'docker build .  -t mohamedhani/nodejs_project'    
            }

        }
      stage ('k8s deployment') 
      {   when { branch 'master' }
          kubernetesDeploy configs: 'k8s_project.yaml',
          kubeconfigId: 'kubeconfig_deployment' 
      }

       
    
}
}
