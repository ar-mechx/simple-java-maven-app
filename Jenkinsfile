pipeline {
   
	agent any

  stages {
       
 stage ('Email notification') {
            steps {
                    echo echo
            }
 }

stage('clean') {
  steps {
           
           sh 'chmod a+x  mvnw' 
          sh './mvnw clean '


  
}
}
stage('Build JAR') {
  steps {
          
           sh 'chmod a+x  mvnw'
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




