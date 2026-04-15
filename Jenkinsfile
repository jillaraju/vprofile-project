pipeline {
    agent any
    tools {
        maven "MAVEN3.9"
        jdk "JDK17"
    }
    
    environment {
        SNAP_REPO = 'vprofile-snapshot'
		NEXUS_USER = 'admin'
		NEXUS_PASS = 'raju'
		RELEASE_REPO = 'vprofile-release'
		CENTRAL_REPO = 'vpro-maven-central'
		NEXUSIP = '172.31.30.174'
		NEXUSPORT = '8081'
		NEXUS_GRP_REPO = 'vpro-maven-group'
        NEXUS_LOGIN = 'nexuslogin'
    }

    stages {
        stage('Build'){
            steps {
                sh 'mvn -s settings.xml -DskipTests install'
            }

            post{
                success{
                    echo "now archiving"
                    archiveArtifacts artifacts: '*/**.war'


                }
            }
      
      
      
        }

        stage('Test'){
          steps {
             sh 'mvn -s settings.xml test'
          }
        }
        
        stage('CheckStleAnalysis'){
           steps {
            sh 'mvn -s settings.xml checkstyle:checkstyle'
           }
         
        }
    }
}