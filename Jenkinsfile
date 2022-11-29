
pipeline {
  agent {
    node {
      label 'slave4567-node'
    }
  }
  stages{
	stage(" Maven Build"){
		steps{
			sh 'mvn clean package'
		}
            }
        stage("Quality Check"){
		steps{
			withSonarQubeEnv('server-sonar') {
				sh "mvn sonar:sonar"
			}
		}
      }
	stage("Upload to Nexus"){
		  steps{
			  nexusArtifactUploader artifacts: [
				  [
					  artifactId: 'DevOpsDemo', 
					  classifier: '', 
					  file: 'target/DevOpsDemo.war', 
					  type: 'war'
				  ]
			  ],
				  credentialsId: 'nexus-sonatype', 
				  groupId: 'com.blazeclan', 
				  nexusUrl: '13.233.25.71:8081', 
				  nexusVersion: 'nexus3', 
				  protocol: 'http', 
				  repository: 'jenkins-assignment3', 
				  version: '1.${BUILD_NUMBER}'
		  }
	  }
  }
}
