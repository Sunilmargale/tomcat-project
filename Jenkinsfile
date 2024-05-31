pipeline {
    agent any
    
    tools {
        maven '3.6.1'
    }
stages{
        stage('Build'){
            steps {
                sh 'mvn clean package -Dmaven.test.skip=true'
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
