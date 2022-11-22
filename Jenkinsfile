pipeline {
   
	agent any
  
  
   
   
        

      environment {
        NEXUS_VERSION = "Nexus3"
        NEXUS_PROTOCOL = "http"
        NEXUS_URL = "http://10.208.202.205:8081/"
        NEXUS_REPOSITORY = "maven-nexus"
        NEXUS_CREDENTIAL_ID = "Nexus_Admin"

        EMAIL_TO = 'sawsan.salaheldin@Etisalat.Com'
        IMAGE_REPO_NAME= 'shoppizer/shoppizer'
        IMAGE_TAG = readMavenPom().getVersion()
        oc_project= 'shoppizer'
        
        oc_username_4=credentials("oc_username_4")
        oc_password_4=credentials("oc_password_4")
      

    

        
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
 stage('Build Docker Image') {
     
   
           steps {
                
              sh """
                    echo 'tag = ${IMAGE_TAG}'
                    echo 'Building the Docker image...'
                    podman build -t default-route-openshift-image-registry.apps.ocp-test.eg01.etisalat.net/${IMAGE_REPO_NAME}:$IMAGE_TAG .
                    echo 'Pushing Docker image to registry...'
                    export KUBECONFIG=/home/jenkins/kubeconfig
                    oc login -u ${oc_username_4} -p ${oc_password_4} https://api.ocp-test.eg01.etisalat.net:6443
                   echo 'OC Password = ${oc_password_4}'
                   echo 'oc_username = ${oc_username_4} '
                """
                   

              
               sh 'podman login -u $(oc whoami)  -p $(oc whoami --show-token) default-route-openshift-image-registry.apps.ocp-test.eg01.etisalat.net --tls-verify=false '


                sh """
                    podman push default-route-openshift-image-registry.apps.ocp-test.eg01.etisalat.net/${IMAGE_REPO_NAME}:$IMAGE_TAG --tls-verify=false

                """
                
                  
              




    }
 }
    stage('Approval Step'){
            steps{
           
                script {
                      emailext mimeType: 'text/html',
                      subject: "$BUILD_NUMBER] Approval for Job [$JOB_NAME]" ,
                      to: "sawsan.salaheldin@Etisalat.Com",
                     body: '''<a href="${BUILD_URL}input">Please click to approve</a>'''
                   env.APPROVED_DEPLOY = input message: 'User input required',
                   parameters: [choice(name: 'Deploy?', choices: 'no\nyes', description: 'Choose "yes" if you want to deploy this build')]
                       }
               
            }
        }


        stage("deploy"){
              when {
                environment name:'APPROVED_DEPLOY', value: 'yes'
            }
            steps{
                sh """
                oc login --insecure-skip-tls-verify -u ${oc_username_4} -p ${oc_password_4} https://api.ocp-test.eg01.etisalat.net:6443
                     
                oc project $oc_project
                oc apply -f oc/deployment4.yaml

                """
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




