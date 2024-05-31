pipeline {
    agent any
    
    tools {
        jdk 'JDK-11'
        maven 'maven-3.6.0'
    }
stages{
        stage('Build'){
            steps {
                sh 'mvn clean package -e -X'
            }
            post {
                success {
                    echo 'Archiving the artifacts'
                    archiveArtifacts artifacts: '**/target/*.war'
                }
            }
        }
        stage ('Deployments'){
                             steps {
                        sshagent(['Tomcat']) {
                       sh "scp -v -o StrictHostKeyChecking=no ./web/target/*.war ec2-user@43.204.111.239:/opt/tomcat/webapps/"
      }
                    }
                }
    }
}
