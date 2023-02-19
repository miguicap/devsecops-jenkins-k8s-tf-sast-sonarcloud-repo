pipeline {
  agent any
  tools { 
        maven 'Maven_3_5_2'  
    }
   stages{
    stage('CompileandRunSonarAnalysis') {
            steps {	
		sh 'mvn clean verify sonar:sonar -Dsonar.projectKey=webdevops-project -Dsonar.organization=webdevops-project -Dsonar.host.url=https://sonarcloud.io -Dsonar.login=acf8bb253651b20c4f245ee3da6928df15842552'
			}
    }

	stage('RunSCAAnalysisUsingSnyk') {
            steps {		
				withCredentials([string(credentialsId: 'SNYK_TOKEN', variable: 'SNYK_TOKEN')]) {
					sh 'mvn snyk:test -fn'
				}
			}
    }		
	stage('Build') { 
            steps { 
               withDockerRegistry([credentialsId: "dockerlogin", url: ""]) {
                 script{
                 app =  docker.build("asg")
                 }
               }
            }
    }

	stage('Push') {
            steps {
                script{
                    docker.withRegistry('659026651741.dkr.ecr.us-east-1.amazonaws.com/asg', 'ecr:us-east-1:aws-migui-credentials') {
                    app.push("latest")a
                    }
                }
            }
    	}
	    
  }
}
