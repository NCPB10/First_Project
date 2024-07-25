pipeline{
    
    agent any
    stages{
        stage('git checkout'){
            steps{
                git branch: 'main', credentialsId: 'jenkins-git', url: 'https://github.com/javahometech/ai-leads'
            }
        }
        stage('mvn build'){
            steps{
                sh 'mvn clean package'
            }
        }
        stage('tomcat deploy'){
            steps{
                sshagent(['tomcat-cred']) {
                // some block
                sh "scp -o StrictHostKeyChecking=no target/ai-leads.war ec2-user@172.31.46.57:/opt/tomcat9/webapps"
                sh "ssh ec2-user@172.31.46.57 /opt/tomcat9/bin/shutdown.sh"
                sh "ssh ec2-user@172.31.46.57 /opt/tomcat9/bin/startup.sh"
                }
                
            }
        }
    }
}
