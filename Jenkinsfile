pipeline {
    agent
      { node 
        {
          label 'deployment_server'
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
      stage ('start docker contrainer') 
      {
           when { branch 'master' }
           steps
           { script{
             try  
              {
                     sh 'docker stop cd_project'
                     sh 'docker rm cd_project'

              } catch (all)	
              {
                echo 'this container not valid'
              }
              sh 'docker run -d --name cd_project -p 3000:3000 mohamedhani/nodejs_project'
            }
          }

       }
    
}
}
