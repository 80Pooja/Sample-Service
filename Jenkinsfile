@Library('java_demo_pipeline@main') _

pipeline { 
    agent { label 'slave4' }
    environment {
        JAVA_HOME = '/usr/lib/jvm/java-17-openjdk-amd64'
        MAVEN_HOME = '/usr/share/maven'
        PATH = "${JAVA_HOME}/bin:${MAVEN_HOME}/bin:${env.PATH}"
    }
    stages {
        stage('Checkout') {             
            steps {
              //  sh "rm -rf Sample-Service"
                //sh "git clone https://github.com/80Pooja/Sample-Service.git"
                //sh "cd Sample-Service"
                 checkoutcode()  
            }
        }
         stage('setupjava17') {
                          steps {
                                   //sh "whoami"
                                   //echo "installing java 17"
                                   //sh "sudo apt update"
                                   //sh "sudo apt install -y openjdk-17-jdk"
                                   setupjava('openjdk-17-jdk')
                          }
                 }
      //  stage('Set up Environment') {
        //    steps {
          //      sh 'export export JAVA_HOME=$(dirname $(dirname $(readlink -f $(which java))))'            
            //    sh 'export MAVEN_HOME=/usr/share/maven'           
          //  }
        //}
stage('setupmaven') {
                 steps {
                         // echo "installing maveen "
                          //sh "sudo apt install -y maven"
                          setupjava('maven')
                 }
        }
        stage('build') {             
            steps {               
               // sh "mvn clean package"
                builtproject()
            }
        }
        stage('Upload Artifact') {
            steps {
                echo 'Uploading artifact...'
                archiveArtifacts artifacts: 'target/simple-parcel-service-app-1.0-SNAPSHOT.jar', allowEmptyArchive: true
            }
        } 
        stage('Run Application') {
            steps {
                echo 'Running Spring Boot application...'
                sh 'mvn spring-boot:run -Dspring-boot.run.arguments="--server.port=8081"'
            } 
        }
}
}
