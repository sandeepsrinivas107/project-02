pipeline {
    agent any
    environment {
        PATH = "/usr/local/src/apache-maven/bin:$PATH"
    }
    stages {
        stage('GitHub Clone') {
            steps {
                git branch: 'project-02', credentialsId: 'github', url: 'https://github.com/sandeepsrinivas107/project-02.git'
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
                url: 'http://3.109.206.200:8080/')], 
                contextPath: 'project-02', 
                war: '**/*.war'
            }
        }
    }
    post {
        success {
            emailext to: "sandeepbuzz1705@gmail.com",
            recipientProviders: [developers()],
            subject: "jenkins Pipe : ${currentBuild.currentResult}: ${env.JOB_NAME}",
            body: "${currentBuild.currentResult}: Job ${env.JOB_NAME}\n More Info can be found here: ${env.BUILD_URL}",
 
            attachLog: true
           
            slackSend message: "Build deployed successfully - Job ${env.JOB_NAME}\n More Info can be found here: ${env.BUILD_URL}"
 
        }
    }
}

 