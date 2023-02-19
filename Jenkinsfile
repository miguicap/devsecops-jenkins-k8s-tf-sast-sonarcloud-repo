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
  }
}
