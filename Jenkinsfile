pipeline {
    agent any

    environment {
        TOMCAT_USER = 'tom'
        TOMCAT_HOST = '192.168.100.59' 
        TOMCAT_PATH = '/opt/tomcat/webapps'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: 'deploy', url: 'https://github.com/GLJ20/simple-maven-app.git'
            }
        }

        stage('Build with Maven') {
            steps {
                sh 'mvn clean package'
            }
        }

        stage('Deploy WAR to Tomcat') {
            steps {
                // Change war file name if needed
                sh """
                    scp target/simple-maven-app-1.0-SNAPSHOT.war ${TOMCAT_USER}@${TOMCAT_HOST}:${TOMCAT_PATH}/app.war
                """
            }
        }

        // stage('Restart Tomcat') {
        //     steps {
        //         sh """
        //             ssh ${TOMCAT_USER}@${TOMCAT_HOST} 'bash -c "sudo systemctl restart tomcat"'
        //         """
        //     }
        // }
    }
}
