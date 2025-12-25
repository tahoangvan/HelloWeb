pipeline {
    agent any

    tools {
        maven 'MAVEN_3'
        jdk 'JDK8'
    }

    stages {
        stage('Build') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
				ssh -o StrictHostKeyChecking=no root@tomcat9 "export JAVA_HOME=/opt/java/openjdk && export JRE_HOME=/opt/java/openjdk && /usr/local/tomcat/bin/shutdown.sh"

                ssh root@tomcat9 "rm -rf /usr/local/tomcat/webapps/com.springmvc3.helloworld*"

                scp /var/jenkins_home/workspace/HelloWeb/target/com.springmvc3.helloworld* root@tomcat9:/usr/local/tomcat/webapps/

                ssh -o StrictHostKeyChecking=no root@tomcat9 "export JAVA_HOME=/opt/java/openjdk && export JRE_HOME=/opt/java/openjdk && /usr/local/tomcat/bin/startup.sh"
                '''
            }
        }
    }
}