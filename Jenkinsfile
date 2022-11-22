pipeline {
   
	agent any

  stages {
       

stage('clean') {
  steps {
           
            
          sh './mvnw clean '
pipeline {
   
	agent any

  stages {
       

stage('clean') {
  steps {
           
            
          sh './mvnw clean '


  
}
}
stage('Build JAR') {
  steps {
          
           
          sh './mvnw  install'



  
}
}
stage("Archive") {
  steps {
        
        archiveArtifacts allowEmptyArchive: false, artifacts: '**/*.jar'
         
        
         
  }
  }
 stage('Build Docker Image') {
     
   
           steps {
                
              sh 'echo echo'



    }
 }
    stage('Approval to deploy to production 2 server') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "v21afahmy15"
                parameters {
                    string(name: 'PERSON', defaultValue: 'RiskTeam', description: 'Deploy to Production server .59?')
                }
            }
            steps {
                echo "Hello, ${PERSON}, nice to meet you."
            }
          }


        stage("deploy"){
              when {
                environment name:'APPROVED_DEPLOY', value: 'yes'
            }
            steps{
                sh 'echo echo'
            }
        }
    }        
 







 
}






  
}
}
stage('Build JAR') {
  steps {
          
           
          sh './mvnw  install'



  
}
}
stage("Archive") {
  steps {
        
        archiveArtifacts allowEmptyArchive: false, artifacts: '**/*.jar'
         
        
         
  }
  }
 stage('Build Docker Image') {
     
   
           steps {
                
              sh 'echo echo'



    }
 }
    stage('Approval Step'){
            steps{
           
            sh 'echo echo'
               
            }
        }


        stage("deploy"){
              when {
                environment name:'APPROVED_DEPLOY', value: 'yes'
            }
            steps{
                sh 'echo echo'
            }
        }
    }        
 







 
}




