pipeline {
    
    agent any 
    
    stages {
        
        stage('code checkout') {
            steps {
                git url: 'https://github.com/L00163565/lab-report-3-software-engineering.git'
            }
        }
        
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn test'
            }
            post {
                always {
                    junit 'target/surefire-reports/*.xml'
                }
            }
        }
        
		stage('Build image') {
            steps{
                script {
                    dockerImage = docker.build registry + ":$BUILD_NUMBER"
                }
            }
        }

        stage('Push Image') {
            steps{
                script {
                docker.withRegistry( "" ) {
                    dockerImage.push()
                    }
                }
            }
        }
    }
}

