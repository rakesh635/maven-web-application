node('master'){

def mvnHome = tool name: 'maven3.6.1', type: 'maven'
    stage('scm checkout'){
    git credentialsId: 'bcbb6f11-2417-4b6c-ac6e-91517a39f4e2', url: 'https://github.com/maven-projects-blr/maven-web-application.git'
   }
    stage('build'){
        sh "${mvnHome}/bin/mvn clean package"
   }
    stage('nexusupload'){
	sh "${mvnHome}/bin/mvn deploy"
	}
    stage('sonarreport'){
	sh "${mvnHome}/bin/mvn sonar:sonar"
        }
	stage('deploytotomcat'){
	sshagent(['tomcat-pipeline']) {
    sh " scp -o StrictHostKeyChecking=no target/*.war ec2-user@18.217.151.48:/opt/apache-tomcat-8.5.42/webapps/
}
  }
}
