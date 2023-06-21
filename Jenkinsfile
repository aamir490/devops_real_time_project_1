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

        //  MODIEFIED SOME FILE : 3
        stage('MODIFIED IMAGE TAG') {
            steps {
                sh '''
                   sed "s/image-name:latest/$JOB_NAME:v1.$BUILD_ID/g" playbooks/dep_svc.yml
                   sed -i "s/image-name:latest/$JOB_NAME:v1.$BUILD_ID/g" playbooks/dep_svc.yml
                   sed -i "s/IMAGE_NAME/$JOB_NAME:v1.$BUILD_ID/g" webapp/src/main/webapp/index.jsp
                   '''
            }            
        }


        // BUILD THE PACKAGE :- 4
        stage('BUILD') {
            steps {
                sh 'mvn clean install package'
            }
        } 





        
    }   // stage close
}  // pipeline close
    

// =========================================== > E N D


      
