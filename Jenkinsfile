pipeline {
    agent
      { node 
        {
          label 'deployment_server'
        }
      } 
    stages {
        stage('Build') {
            when { brnach 'master' }
            steps {
                 sh 'docker build -t workflow_system:0.2'
            }

        }
        stage ('build docker image'){
            when { branch 'master'}
            steps    
            { 
               sh 'docker run -d -p 3000:3000 --name nodejs workflow:0.2'
            }

        }

       
    
}
}
