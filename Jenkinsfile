pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                git 'https://github.com/chfu88/jenkins-ansible-javaapp.git'

                sh "mvn -f app/pom.xml -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                    archiveArtifacts 'app/target/*.war'
                }
            }
        }
        stage('deploy'){
            steps{
                ansiblePlaybook credentialsId: 'webhostid', installation: 'ansible', inventory: 'deployment/environment.ini', playbook: 'deployment/tomcat.yml'
            }
        }
    }
}
