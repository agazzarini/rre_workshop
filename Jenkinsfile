pipeline {
    agent any
//     tools {
//         maven 'apache-maven-3.5.4'
//     }
    stages {
//         stage('Validate') {
//             steps {
//                 sh 'mvn dependency:purge-local-repository'
//                 sh 'mvn clean validate'
//             }
//         }
        stage('Compile') { 
            steps {
                sh 'mvn compile' 
            }
        }
        stage('Test') {
            steps {
                sh 'mvn test'
            }
        }
         stage('Install') {
                    steps {
                        sh 'mvn install'
                    }
         }
    }
}