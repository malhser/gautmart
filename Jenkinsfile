pipeline {
    agent any

//	tools {
//		jdk 'jdk8'
//	}
//	environment {
//		M2_INSTALL = "/usr/bin/mvn"
//	}

    stages {
        stage('Clone-Repo') {
	    	steps {
	        	checkout scm
	    	}
        }

        stage('Build') {
            steps {
                sh 'mvn install -Dmaven.test.skip=true'
            }
        }
		
        stage('Unit Tests') {
            steps {
                sh 'mvn compiler:testCompile'
                sh 'mvn surefire:test'
                junit 'target/**/*.xml'
            }
        }

        stage('Deployment') {
            steps {
                sh 'sshpass -p "wiculty" scp target/gamutkart.war wiculty@10.88.0.1:/home/lokesh/Templates/gamutkart2/apache-tomcat-8.5.38/webapps'
                sh 'sshpass -p "wiculty" ssh wiculty@10.88.0.1 "/home/lokesh/Templates/gamutkart2/apache-tomcat-8.5.38/bin/startup.sh"'
            }
        }
    }
}
