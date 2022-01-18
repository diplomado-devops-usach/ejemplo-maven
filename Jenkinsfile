pipeline {
    agent any

    stages {
        stage('Compile') {
            steps {
                sh 'mvn clean compile -e'
            }
        }
		
		stage('Sonar') {
			steps {
				script{
					def scannerHome = tool 'sonar-scanner';
					withSonarQubeEnv('sonar-server') {
						sh "${scannerHome}/bin/sonar-scanner -Dsonar.projectKey=ejemplo-maven -Dsonar.sources=src -Dsonar.java.binaries=build"
					}
				}
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
                sleep 30
            }
        }
        
        stage('RunTest') {
            steps {
                   sh 'curl http://localhost:8081/rest/mscovid/test?msg=testing'
            }
        }
    }
}

