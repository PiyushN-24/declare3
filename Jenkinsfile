pipeline {
    agent any
    
    stages {
        stage('CheckOut') {
            steps {
                checkout scm
            }
        }
        stage('Validate') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn validate'
            }
        }
	stage('Compile') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn compile'
            }
        }
	stage('Test') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn test'
            }
        }
	stage('Package') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn package'
            }
        }
	stage('Verify') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn verify'
            }
        }
	stage('Install') {
            steps {
                sh '/home/therecker/DevOps/Maven/apache-maven-3.9.6/bin/mvn install'
            }
        }
        stage('Deployment') {
            steps {
                sh 'cp target/declare3.war /home/therecker/DevOps/Maven/apache-tomcat-9.0.85/webapps/'
            }
        }
    }
    post {
        success {
            emailext (
                to: 'awspiyush189@gmail.com', // Email recipient(s)
                subject: "Build Successful: ${currentBuild.fullDisplayName}", // Email subject
                body: "The build ${currentBuild.fullDisplayName} completed successfully. You can access the artifacts at ${env.BUILD_URL}", // Email body
            )
        }
        failure {
            emailext (
                to: 'awspiyush189@gmail.com',
                subject: "Build Failed: ${currentBuild.fullDisplayName}",
                body: "The build ${currentBuild.fullDisplayName} failed. Please check the Jenkins logs for more details: ${env.BUILD_URL}",
            )
        }
    }
}
