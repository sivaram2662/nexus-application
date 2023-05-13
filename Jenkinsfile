// pipeline {
//     agent any

//     stages {
//         stage('checkout') {
//             steps {
//                 git branch: 'main', url: 'git@github.com:sivaram2662/sparkjava-application.git'
//             }
//         }
//          stage('maven-build') {
//             steps {
//                 sh '/opt/maven/bin/mvn clean package'
//             }
//         }
//         // stage('Upload files to Nexus') {
//         //     steps {
//         //         nexusArtifactUploader artifacts: [
//         //             [
//         //                 artifactId: 'sparkjava-hello-world',
//         //                 classifier: '',
//         //                 file: "/var/lib/jenkins/workspace/java-war-ci-job/target/sparkjava-hello-world-1.0.war",
//         //                 type: 'war'
//         //             ]
//         //         ],
//         //         credentialsId: 'nexus3',
//         //         groupId: 'sparkjava-hello-world',
//         //         nexusUrl: '172.31.24.231:8081',
//         //         nexusVersion: 'nexus3',
//         //         protocol: 'http',
//         //         repository: 'jenkins-ci',
//         //         version: '1.0.${BUILD_NUMBER}'
//         //     }
//         // }
//     }
// }


pipeline{
    agent any
    // environment {
    //     PATH = "$PATH:/opt/apache-maven-3.8.2/bin"
    // }
    stages{
       stage('GetCode'){
            steps{
               git branch: 'main', url: 'git@github.com:sivaram2662/sparkjava-application.git'
            }
         }        
       stage('Build'){
            steps{
                sh '/opt/maven/bin/mvn clean package'
            }
         }
        stage('SonarQube analysis') {
//    def scannerHome = tool 'SonarScanner 4.0';
        steps{
        withSonarQubeEnv('sonarqube-8.3') { 
        // If you have configured more than one global server connection, you can specify its name
//      sh "${scannerHome}/bin/sonar-scanner"
        sh "mvn sonar:sonar"
    }
        }
        }
       
    }
}