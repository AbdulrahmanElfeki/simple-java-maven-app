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
                sh 'jar cvf my-app.war .'
                sh 'ls -la'
            }
        }
        stage('Deployment') { 
            steps{
                deploy adapters: [tomcat9(url:'http://52.54.249.228:8080/',credentialsId:'tomcat-cred')],
                war: 'target/*.war'
            }
        }
            }
        }
