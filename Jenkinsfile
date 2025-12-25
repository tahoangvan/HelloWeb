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
                ssh root@debian "systemctl stop tomcat9"

                ssh root@debian "rm -rf /opt/tomcat9/webapps/com.springmvc3.helloworld*"

                scp target/com.springmvc3.helloworld.war root@debian:/opt/tomcat9/webapps/

                ssh root@debian "systemctl start tomcat9"
                '''
            }
        }
    }
}