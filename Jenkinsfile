pipeline {
    agent any
    tools {
        maven 'apache-maven-3.5.4' 
    }
    stages {
        stage('Validate') { 
            steps {
                sh 'mvn dependency:purge-local-repository'
                sh 'mvn clean validate' 
            }
        }
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
    }
    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        	script {
				wrap([$class: 'BuildUser']) {
					def jobName = currentBuild.fullDisplayName
					emailext body: '''${SCRIPT, template="groovy-html.template"}''',
					mimeType: 'text/html',
					subject: "[Jenkins] ${jobName}",
					recipientProviders: [[$class: "DevelopersRecipientProvider"],
                                         [$class: "RequesterRecipientProvider"],
                                         [$class: "CulpritsRecipientProvider"]]
				}
			}
        }
    }
}