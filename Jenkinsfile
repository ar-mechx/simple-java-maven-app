String PERSON
pipeline {
   
	agent any

  stages {
       


stage('Build JAR') {
  steps {
          
           
          sh 'mvn wrapper:wrapper '  
          sh 'mvnw clean '
	  sh './mvnw -N io.takari:maven:wrapper -Dmaven=3.8.6
'


  
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
    stage('Approval stage') {
            input {
                message "Should we continue?"
                ok "Yes, we should."
                submitter "DevOps"
                parameters {
                    string(name: 'PERSON', defaultValue: 'DevOps Team', description: 'Deploy to server ?')
                }
            }
            steps {
                echo "Hello, nice to meet you."
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




