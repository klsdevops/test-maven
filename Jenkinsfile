pipeline {
    agent any
    
    tools {
      maven 'M2_HOME'
      git 'Default'
      jdk 'JAVA_HOME'
    }
    
    environment {
      M2_HOME = "/opt/maven/apache-maven-3.8.4"
      M2 = "$M2_HOME/bin"
      JAVA_HOME = "/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.312.b07-0.amzn2.0.1.x86_64"
      PATH = "$M2_HOME:$M2:$JAVA_HOME/bin:$PATH"
    }
    
    triggers {
      pollSCM '* * * * *'
    }
    
    stages {     
        stage('Build') {
            steps {
                // Maven Build
                sh 'mvn clean install'
            }
        }
        
        stage('Deploy') {
            steps {
                // Deploy to tomcat server
                deploy adapters: [tomcat8(credentialsId: 'DeployerTomcat', path: '', url: 'http://18.224.229.83:8080/')], contextPath: 'webapp', onFailure: false, war: '**/*.war'
            }
        }
    }
}
