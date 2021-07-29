pipeline {
    agent any
    
    triggers{
        pollSCM('* * * * *')
    }

    tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "apache-maven-3.8.1"
    }

    stages {
        stage('Build') {
            steps {
                bat 'mvn spring-javaformat:apply'
                bat 'mvn clean package'
            }

            post {
                // If Maven was able to run the tests, even if some of the test
                // failed, record the test results and archive the jar file.
                success {
                    junit '**/target/surefire-reports/*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }
    }
}