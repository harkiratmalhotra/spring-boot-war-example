pipeline {
    agent any
    tools {
        maven 'Maven'
    }
    stages {
        stage('Test') {
            steps {
               sh 'mvn test' 
            }
        }
        stage('Build') {
            steps {
               sh 'mvn install'
            }
        }
        stage('Deploy on Test') {
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://10.0.2.4:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
        stage('Deploy on Prod') {
            input {
                message 'Do you want todeploy on Prod ?'
                ok 'Yes'
            }
            steps {
               deploy adapters: [tomcat9(credentialsId: 'tomcat9', path: '', url: 'http://10.0.2.4:8080')], contextPath: '/app', war: '**/*.war'
            }
        }
    }
    post {
        always {
            echo 'I will always run'
        }
        success {
            echo 'I will run on success of each stages'
        }
        failure {
            echo 'I will run if any of the stages fails'
        }
    }
}
