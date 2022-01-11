pipeline{
    agent{
        label "aws"
    }
    tools{
        maven 'mavenhome' 
    }
    stages{
        stage("Test"){
            steps{
                sh "mvn --version"
                sh 'mvn test'
            }  
        }
        stage("Build"){
            steps{
                sh 'mvn package'
            }  
        }
        stage("Deploy"){
            steps{
                deploy adapters: [tomcat9(credentialsId: '5f91bcd4-9eb2-4549-82db-7ea46f48cde5', path: '', url: 'http://3.138.109.59:8081')], contextPath: 'MyApp', war: '**/*.war'
            }  
        }
    }
    post{
        always{
            echo "========always========"
        }
        success{
            echo "========pipeline executed successfully ========"
        }
        failure{
            echo "========pipeline execution failed========"
        }
    }
}

