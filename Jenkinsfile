pipeline{
    agent any
    stages{
        
        stage('Package and Nexus Deploy') {
            steps {
                sh script: 'mvn clean deploy'
            }
        }
        
        stage('Deploy to Tomcat') {
            steps {
                sshagent(['Tomcat-cred']) {
                    sh script: 'scp ssh -o StrictHostKeyChecking=no target/israqua.war ec2-user@52.167.158.215:/opt/tomcat8/webapps/'
                    sh script: 'ssh ec2-user@52.167.158.215 service tomcat stop'
                    sh script: 'ssh ec2-user@52.167.158.215 service tomcat start'
                }
            }
        }
    }
}
