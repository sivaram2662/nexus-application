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
                sh '/opt/apache-maven-3.9.2/bin/mvn clean package'
            }
        }
        stage('Upload files to Nexus') {
            steps {
                nexusArtifactUploader artifacts: [
                    [
                        artifactId: 'sparkjava-hello-world',
                        classifier: '',
                        file: "/var/lib/jenkins/workspace/java-war-ci-job/target/sparkjava-hello-world-1.0.war",
                        type: 'war'
                    ]
                ],
                credentialsId: 'nexus3',
                groupId: 'sparkjava-hello-world',
                nexusUrl: '172.31.24.231:8081',
                nexusVersion: 'nexus3',
                protocol: 'http',
                repository: 'jenkins-repo',
                version: '1.0.${BUILD_NUMBER}'
            }
        }
    }
}


