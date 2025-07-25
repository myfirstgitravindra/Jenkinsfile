pipeline {
    agent any
    environment {
        Tomcat_user = "ec2-user"
        Tomcat_IP   = "13.218.160.151"
    }
    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/myfirstgitravindra/maventomcat.git'
            }
        }
        stage('maven build') {
            steps {
             sh 'mvn clean package '
            }
        }
        stage('tomcat deploy') {
            steps {
             sshagent(['tomcat-cred']) {
    sh "scp -o StrictHostKeyChecking=no target/*.war ${Tomcat_user}@${Tomcat_IP}:/opt/tomcat10/webapps/"
                    // Stop and start Tomcat
                    sh "ssh ${Tomcat_user}@${Tomcat_IP} sudo /opt/tomcat10/bin/shutdown.sh"
                    sh "ssh ${Tomcat_user}@${Tomcat_IP} sudo /opt/tomcat10/bin/startup.sh"
}
            }
        }
    }
}
