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
        stage('Deployment') { 
            steps {
                deploy adapter: [tomcat9(url:'http://52.54.249.228:8080/',credentialsId: "tomcat-cred")]
            }
        }
    }
}
