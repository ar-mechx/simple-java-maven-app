pipeline {
    
    agent any 
    
    stages {
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
}
