pipeline{
    agent{
        label "aws1"
    }
    tools{
        maven 'mavenhome' 
    }
    stages{
        stage("Test"){
            steps{
                sh "mvn --version"
                slackSend channel: 'jenkinsnotification', message: 'Job Started'
            }  
        }
        stage("Build"){
            steps{
                sh 'mvn package'
            }  
        }
        stage("Deploy on Dev"){
            steps{
		 
                deploy adapters: [tomcat9(credentialsId: '48cad2b3-6227-489d-83a4-e3508346fbc3', path: '', url: 'http://18.191.122.250:8080')], contextPath: 'Hello-Dev', war: '**/*.war'
            }  
          }
        stage("Deploy on Test"){
            steps{
                deploy adapters: [tomcat9(credentialsId: '48cad2b3-6227-489d-83a4-e3508346fbc3', path: '', url: 'http://18.191.122.250:8080')], contextPath: 'Hello-Test', war: '**/*.war'
            }  
         }
	  stage("Deploy on PROD"){
		  input{
			  message "should we continue"
			  ok "Yes we should"
		  }
			
            steps{
                deploy adapters: [tomcat9(credentialsId: '48cad2b3-6227-489d-83a4-e3508346fbc3', path: '', url: 'http://18.191.122.250:8080')], contextPath: 'Hello-Prod', war: '**/*.war'
            }  
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            slackSend channel: 'jenkinsnotification', message: 'Job Completed'
        }
        failure{
            slackSend channel: 'jenkinsnotification', message: 'Job Failed'
        }
    }
}
