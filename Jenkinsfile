pipeline {
    agent {
        node {
            label 'docker' && 'maven'
        }
    }
    stages { 	
        stage('Build Jar') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }
        stage('Build Image') {
            steps {
                script {
                	app = docker.build("localhost:3000/vinsdocker/containertest")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
			        docker.withRegistry('http://localhost') {
			        	app.push("${BUILD_NUMBER}")
			            app.push("latest")
			        }
                }
            }
        }        
    }
}