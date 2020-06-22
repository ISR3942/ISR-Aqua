pipeline{
    agent any
    environment {
        TOMCAT_HOST = "ec2-user@52.167.158.215"
        TOMCAT_SVC = "service tomcat"
    }
    stages{
        
        stage('Package and Nexus Deploy') {
            steps {
                sh script: 'mvn clean deploy1'
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
                sshagent(['Tomcat-cred']) {
                    sh script: "scp -o StrictHostKeyChecking=no target/israqua.war ${TOMCAT_HOST}:/opt/tomcat8/webapps/"
                    sh script: "ssh ${TOMCAT_HOST} ${TOMCAT_SVC} stop"
                    sh script: "ssh ${TOMCAT_HOST} ${TOMCAT_SVC} start"
                }
            }
        }
    }
    
    post {
      failure {
        mail bcc: '', body: 'Hello, your job said thusssssssssss', 
             cc: '', from: '', replyTo: '', subject: 'Job failed', 
             to: 'indukurisriramaraju7@gmail.com'
      }
    }
}
