pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                sh 'mvn clean compile -e'
            }
        }
        
        stage('Test') {
            steps {
                sh 'mvn clean test -e'
            }
        }
        
        stage('Package') {
            steps {
                sh 'mvn clean package -e'
            }
        }
        
        stage('Run') {
            steps {
                sh 'nohup mvn spring-boot:run > server.log 2>&1&'
                sleep 60
            }
        }
        
        stage('RunTest') {
            steps {
                   sh 'curl http://localhost:8081/rest/mscovid/test?msg=testing'
            }
        }
    }
}

