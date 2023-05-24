pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                git branch: 'main', url: 'git@github.com:sivaram2662/sparkjava-application.git'
            }
        }
        stage('maven-build') {
            steps {
                sh 'mvn clean package'
            }
        }
        stage('Upload files to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'sparkjava-hello-world',
                        classifier: '',
                        file: "/var/lib/jenkins/workspace/pipeline/target/sparkjava-hello-world-1.0.war",
                        type: 'war'
                    ]
                ],
                credentialsId: 'nexus',
                groupId: 'sparkjava-hello-world',
                nexusUrl: '10.0.4.157:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'maven-hosted-code',
                version: '1.0.${BUILD_NUMBER}'
            }
        }
          stage('Deploy to Tomcat server') {
            steps {
                sh 'curl -u admin:admin@123 -O http://nexus.siva.quest/repository/maven-hosted-code/sparkjava-hello-world/sparkjava-hello-world/1.0.4/sparkjava-hello-world-1.0.4.war'
            }
        }
    }
} 



