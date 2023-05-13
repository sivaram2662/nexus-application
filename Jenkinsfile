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




pipeline {
    agent any
    stages {
        stage('SCM') {
            steps {
                 git branch: 'main', url: 'git@github.com:sivaram2662/sparkjava-application.git'
            }
        }
        stage('build && SonarQube analysis') {
            steps {
                withSonarQubeEnv('My SonarQube Server') {
                    // Optionally use a Maven environment you've configured already
                    withMaven(maven:'Maven 3.9.2') {
                        sh '/opt/maven/bin/mvn clean package sonar:sonar'
                    }
                }
            }
        }
        stage("Quality Gate") {
            steps {
                timeout(time: 1, unit: 'HOURS') {
                    // Parameter indicates whether to set pipeline to UNSTABLE if Quality Gate fails
                    // true = set pipeline to UNSTABLE, false = don't
                    waitForQualityGate abortPipeline: true
                }
            }
        }
    }
}