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
                	app = docker.build("vinsdocker/containertest")
                }
            }
        }
        stage('Push Image') {
            steps {
                script {
			        docker.withRegistry('http://localhost:3000') {
			            app.push("latest")
			        }
                }
            }
        }        
    }
    post{
      always {
         sh "docker rmi \$(docker images -qa -f 'dangling=true') || exit 0"
         sh "docker system prune -f"
      }   
   }    
}