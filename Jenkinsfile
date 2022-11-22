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
                
              echo echo



    }
 }
    stage('Approval Step'){
            steps{
           
            echo echo
               
            }
        }


        stage("deploy"){
              when {
                environment name:'APPROVED_DEPLOY', value: 'yes'
            }
            steps{
                echo echo
            }
        }
    }        
 







  post { 
        always { 
            echo 'I will always run, and I can clean up the workspace here......'
        }
        success {
            echo 'I will run in case of failure, and I will send an email in case of failure.'
            mail bcc: '', body: """Dears,
            Congratulations the build # $BUILD_NUMBER for the Job [$JOB_NAME] has successded.
            Below are the Build details:
            Build Number : $BUILD_NUMBER
            Build URL is : $BUILD_URL
            Build Tag : $BUILD_TAG
            Node Name : $NODE_NAME
            Executor Number : $EXECUTOR_NUMBER
            Workspace : $WORKSPACE
            Thanks. """, cc: '', from: '', replyTo: '', subject: "Build # [$BUILD_NUMBER] triggered for Job [$JOB_NAME] >> Success", to: "$EMAIL_TO"

            
        }
        failure { 
            echo 'I will run in case of success, and I will send an email in case of success'
            mail bcc: '', body: """Dears,
            Unfortunately the build # $BUILD_NUMBER for the Job [$JOB_NAME] has failed.
            Below are the Build details:
            Build Number : $BUILD_NUMBER
            Build URL is : $BUILD_URL
            Build Tag : $BUILD_TAG
            Node Name : $NODE_NAME
            Executor Number : $EXECUTOR_NUMBER
            Workspace : $WORKSPACE
            Thanks. """, cc: '', from: '', replyTo: '', subject: "Build # [$BUILD_NUMBER] triggered for Job [$JOB_NAME] >> Failed", to: "$EMAIL_TO"

       
        }

}
}




