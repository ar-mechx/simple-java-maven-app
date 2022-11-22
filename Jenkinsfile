pipeline {
   
	agent any

  stages {
       

stage('clean') {
  steps {
           
            
          sh 'mvnw clean '


  
}
}
stage('Build JAR') {
  steps {
          
           
          sh 'mvnw  install'



  
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




