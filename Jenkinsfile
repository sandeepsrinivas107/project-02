pipeline {
    agent any
    environment {
        PATH = "/usr/local/src/apache-maven/bin:$PATH"
    }
    stages {
        stage('GitHub Clone') {
            steps {
                git branch: 'project-02', url: 'https://github.com/sandeepsrinivas107/project-02.git'
            }
        }
        stage('Build Maven') {
            steps {
                sh "mvn clean package"
            }
        }
        stage('Deploy Tomcat') {
            steps {
                deploy adapters: [tomcat9(alternativeDeploymentContext: '', credentialsId: 'Tomcat-01-key', 
                path: '', 
                url: 'http://65.1.132.127:8080/')], 
                contextPath: 'project-02', 
                war: '**/*.war'
            }
        }
    }
}

 