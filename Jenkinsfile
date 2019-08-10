node('master'){

def mvnHome = tool name: 'maven3.6.1', type: 'maven'

    stage('scm checkout'){
    git credentialsId: 'fdd20077-d9e7-4815-a9eb-79a64db504eb', url: 'https://github.com/maven-projects-blr/maven-web-application.git'
   }

    stage('build'){
        sh "${mvnHome}/bin/mvn clean package"
   }

    stage('nexusupload'){
	sh "${mvnHome}/bin/mvn deploy"
	}

    stage('sonarreport'){
	sh "${mvnHome}/bin/mvn sonar:sonar"

       	stage('deploytotomcat'){
	sshagent(['tomcat-pipeline']) {
    sh " scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.216.192.250:/opt/apache-tomcat-8.5.42/webapps/maven-web-application.war "
}
  } 
    }
