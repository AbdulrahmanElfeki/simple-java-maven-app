pipeline {
    agent {label 'maven'}
    environment {
        PATH = "/opt/apache-maven-3.9.8/bin:$PATH"
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
        stage('test') {
            steps {
                sh "mvn surefire-report:report"
            }
        }
        stage('Archive artifact'){
            steps{
                archiveArtifacts artifacts: 'target/*.jar'
            }
        }
        stage('Deployment') { 
            sshagent(['ssh-key-tomcat']) {
            sh 'scp jenkins/workspace/FirstMavenProject/my-app-1.0-SNAPSHOT.jar ec2-user@10.1.1.63:/opt/apache-tomcat-9.0.93/webapps/'
            sh 'ssh ec2-user@10.1.1.63 "sudo /opt/apache-tomcat-9.0.93/bin/catalina.sh stop " '
            sh 'ssh ec2-user@10.1.1.63 "sudo /opt/apache-tomcat-9.0.93/bin/catalina.sh start " '
        }
            }
        }
    }
}
