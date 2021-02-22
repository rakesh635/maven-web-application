node('master'){

def mvnHome = tool name: 'maven-3.6.1', type: 'maven'

    stage('scm checkout'){
    git credentialsId: 'xx-xxx-xxxx', url: 'https://github.com/maven-projects-blr/maven-web-application.git'
   }

    stage('build'){
        sh "${mvnHome}/bin/mvn clean package"
   }

    stage('nexusupload'){
	sh "${mvnHome}/bin/mvn deploy"
	}

    stage('deploytotomcat'){
	sshagent(['tomcat-pipeline']) {
    sh " scp -o StrictHostKeyChecking=no target/maven-web-application.war ec2-user@18.216.192.250:/opt/apache-tomcat-8.5.42/webapps/maven-web-application.war "
}
  } 
    }

