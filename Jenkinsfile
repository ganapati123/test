pipeline{
    agent any
    stages{
        stage("Git Checkout"){
            steps{
                git credentialsId: 'Java', url: 'https://github.com/ganapati123/test.git'
            }
        }
        stage("Maven Build"){
            steps{
                sh "mvn clean package"
                sh "mv target/*.war target/myweb.war"
            }
        }
        stage("deploy-dev"){
            steps{
                sshagent(['tomcat-new']) {
                sh """
                    scp -o StrictHostKeyChecking=no target/myweb.war  ubuntu@172.31.22.241:/home/ubuntu/apache-tomcat-10.0.22/webapps/
                    
                    ssh ubuntu@172.31.22.241 /home/ubuntu/apache-tomcat-10.0.22/bin/shutdown.sh
                    
                    ssh ubuntu@172.31.22.241 /home/ubuntu/apache-tomcat-10.0.22/bin/startup.sh
                
                """
            }
            
            }
        }
    }
}
