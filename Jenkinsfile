// =========================================== > s t a r t

pipeline { // pipeline  start

    agent any
    
    // MAVEN CMND PATH :-
    environment {
      PATH = "$PATH:/opt/apache-maven/bin/"
    }

  environment {
    DOCKERHUB_USER = credentials('dockerhub-username')
    DOCKERHUB_PASS = credentials('dockerhub-password')
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

        // SONAR REPORT EXECUTION :  5   sqa_fadf6de91f2cdb50fbf1764e33a074c5dc85585a
        stage('SONAR SCANNER') {
            environment {
            sonar_token = credentials('SONAR_TOKEN')
            }
            steps {
                sh 'mvn sonar:sonar -Dsonar.projectName=$JOB_NAME \
                    -Dsonar.projectKey=$JOB_NAME \
                    -Dsonar.host.url=http://172.31.6.80:9000 \
                    -Dsonar.token=$sonar_token'
            }
        } 

        // COPY JAR TO DOCKERHUB : 6
        stage('COPY JAR & DOCKERFILE') {
            steps {
                sh 'ansible-playbook playbooks/create_directory.yml'
            }
        }


    stage('Build and Push Image') {
      steps {
        script {
          sh '''
            cd /opt/docker
            docker build -t ${JOB_NAME}:v1.${BUILD_ID} .
            docker tag ${JOB_NAME}:v1.${BUILD_ID} sunnydevops2022/${JOB_NAME}:v1.${BUILD_ID}
            docker tag ${JOB_NAME}:v1.${BUILD_ID} sunnydevops2022/${JOB_NAME}:latest
            echo ${DOCKERHUB_PASS} | docker login -u ${DOCKERHUB_USER} --password-stdin
            docker push sunnydevops2022/${JOB_NAME}:v1.${BUILD_ID}
            docker push sunnydevops2022/${JOB_NAME}:latest
            docker rmi -f $(docker images sunnydevops2022/${JOB_NAME} -a -q)
            docker logout
          '''
        }
      }


  
 


















        
    
















        
        
    }   // stage close
}  // pipeline close
    

// =========================================== > E N D


      
