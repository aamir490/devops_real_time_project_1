// =========================================== > s t a r t

pipeline { // pipeline  start

    agent any
    
    // MAVEN CMND PATH :-
    environment {
      PATH = "$PATH:/opt/apache-maven-3.9.2/bin"
    }
    
    stages {  // stage start

        //  1
        stage('CLEAN WORKSPACE') {
            steps {
                cleanWs()
            }
        }

      // 2
        stage('CODE CHECKOUT') {
            steps {
                git 'https://github.com/aamir490/devops_real_time_project_1.git'
            }
        }




      

    }   // stage close
}  // pipeline close
    

// =========================================== > E N D


      
