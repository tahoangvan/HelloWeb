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
				ssh -o StrictHostKeyChecking=no root@tomcat9 "export JAVA_HOME=/usr/local/openjdk-8/bin/java && export JRE_HOME=/usr/local/openjdk-8/bin/java && /usr/local/tomcat/bin/shutdown.sh || true"

                ssh root@tomcat9 "rm -rf /usr/local/tomcat/webapps/com.springmvc3.helloworld*"

                scp /var/jenkins_home/workspace/HelloWeb/target/com.springmvc3.helloworld-0.0.1.war root@tomcat9:/usr/local/tomcat/webapps/root.war

                ssh -o StrictHostKeyChecking=no root@tomcat9 "export JAVA_HOME=/usr/local/openjdk-8/bin/java && export JRE_HOME=/usr/local/openjdk-8/bin/java && /usr/local/tomcat/bin/catalina.sh start"
                '''
            }
        }
    }
}