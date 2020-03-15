pipeline {
    agent any

	tools {
		maven 'maven3.6'
	}
//
//	environment {
//		M2_INSTALL = "/home/gamut/Distros/apache-maven-3.6.0/bin/mvn"
//	}

    stages {
		stage('Clone-Repo') {
			steps {
				checkout scm
			}
		}
		stage('Build') {
	    	steps {
				sh 'mvn install -DskipTests'
			}
	    }
		stage('Unit Tests') {
			steps {
				sh 'mvn surefire:test'
			}
		}
		stage('Deployment') {
	    	steps {
				print "Deployment is done!"
				sh 'sshpass -p "gamut" scp target/gamutkart.war gamut@172.17.0.3:/home/gamut/distros/apache-tomcat-9.0.31/webapps'
				sh 'sshpass -p "gamut" ssh -o StrictHostKeyChecking=no gamut@172.17.0.3 "JAVA_HOME=/home/gamut/builds/jdk8" "/home/gamut/distros/apache-tomcat-9.0.31/bin/startup.sh"'	


	    	}
		}
    }
}
