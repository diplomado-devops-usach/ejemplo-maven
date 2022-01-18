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

	stage('uploadNexus') {
		steps {
			nexusArtifactUploader artifacts: [[artifactId: 'DevOpsUsach2020', classifier: '', file: '/diplomado/modulo3/ejemplo-maven/build/DevOpsUsach2020-0.0.1.jar', type: 'jar']], credentialsId: 'nexus-usd-credentials', groupId: 'com.devopsusach2020', nexusUrl: 'localhost:8081', nexusVersion: 'nexus3', protocol: 'http', repository: 'test-nexus', version: '0.0.1'
		}
	}
    }
}

