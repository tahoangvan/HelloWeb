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
				ssh root@tomcat9 "export JAVA_HOME=/opt/java/openjdk && export JRE_HOME=/opt/java/openjdk && /usr/local/tomcat/bin/shutdown.sh"

                ssh root@tomcat9 "rm -rf /usr/local/tomcat/webapps/com.springmvc3.helloworld*"

                scp target/com.springmvc3.helloworld.war root@tomcat9:/usr/local/tomcat/webapps/

                ssh root@tomcat9 "export JAVA_HOME=/opt/java/openjdk && export JRE_HOME=/opt/java/openjdk && /usr/local/tomcat/bin/startup.sh"
                '''
            }
        }
    }
}