pipeline {
    agent any
	
    stages {
        stage('Build Application') {
	    tools {
        maven 'Maven'
            }
            steps {
		 
                sh 'mvn -f java-tomcat-sample/pom.xml clean package'
            }
	    
            post {
                success {
                    echo "Now Archiving the Artifacts...."
                    archiveArtifacts artifacts: '**/*.war'
                }
            }
        }
        stage('Deploy in Staging Environment'){
            steps{
                build job: 'deploy_appl_stag'

            }
            
        }
        stage('Deploy to Production'){
            steps{
                timeout(time:5, unit:'DAYS'){
                    input message:'Approve PRODUCTION Deployment?'
                }
                build job: 'Deploy_Appln_Prod'
            }
        }
    }
}
