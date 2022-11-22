pipeline {
   
	agent any
    

        
        }

  stages {
       
 stage ('Email notification') {
            steps {
                    echo '>>> Send New application build notification'
                    //mail bcc: '', body: 'Thanks', cc: '', from: '', replyTo: '', subject: "New Build # [$BUILD_NUMBER] triggered for Job [$JOB_NAME]", to: ${EMAIL_TO}
                    mail bcc: '', body: """Dears,
                    A new build has been started for the Job [$JOB_NAME].
                    Below are the Build details:
                    Build Number : $BUILD_NUMBER
                    Build URL is : $BUILD_URL
                    Build Tag : $BUILD_TAG
                    Node Name : $NODE_NAME
                    Executor Number : $EXECUTOR_NUMBER
                    Workspace : $WORKSPACE
                    Thanks. """, cc: '', from: '', replyTo: '', subject: "New Build # [$BUILD_NUMBER] triggered for Job [$JOB_NAME]", to: "$EMAIL_TO"
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


    }  
