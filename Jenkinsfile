pipeline{
	agent any;

	tools {
			maven "MVN"
	}

	stages{
		stage('checkout'){
				steps{
					echo "Checkout the code from SCM"
					git branch: 'main', url: 'https://github.com/devopss1/brilliusnov22.git'
				}
		}
		stage('build'){
				steps{
					echo "Build the code"
				//	sh 'mvn -f myapp/ clean package'
				}
		}
		stage('Upload to artifactory repository'){
				steps{
					echo "Nexus"
					nexusArtifactUploader artifacts: [[artifactId: 'myapp', classifier: '', file: '/var/lib/jenkins/workspace/scripted-pipeline/myapp/target/myapp.war', type: 'war']], credentialsId: '7c8abf4d-b47a-4f57-9e6a-70711397d741', groupId: 'brillius.app1', nexusUrl: '192.168.0.12:8081/nexus', nexusVersion: 'nexus2', protocol: 'http', repository: 'snapshots', version: '1.0-SNAPSHOT'
				}
		}
		stage('deploy'){
				steps{
					echo "Deploy"
					sh '''cp /var/lib/jenkins/workspace/scripted-pipeline/myapp/target/myapp.war /tmp/dir1/apache-tomcat-9.0.69/webapps/
/tmp/dir1/apache-tomcat-9.0.69/bin/shutdown.sh
sleep 20
/tmp/dir1/apache-tomcat-9.0.69/bin/startup.sh

'''
				}
	    post{
		    success {
					echo "send notification to DL"
	    	}
		failure{
				echo "Pipeline failed"
		    }
	    }
		}
	}
}

