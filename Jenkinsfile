pipeline {
    agent any
    tools {
        maven 'maven3.8.6'
        jdk 'jdk'
    }
    stages {

        stage('Prepare SCM') {
            steps {
                git branch: 'master', url: 'https://github.com/praveenkumar1290/sonar-coverage-example-java.git'
            }
        }
        stage ('Build') {
            steps {
                bat 'mvn -Dmaven.test.failure.ignore=true install' 
            }
            post {
                success {
                    junit 'target/surefire-reports/**/*.xml' 
                }
            }
        }
        stage('Sonarqube') {
            environment {
                scannerHome = tool 'sonarqube'
            }
            steps {
                withSonarQubeEnv('sonarqube') {
                    bat 'C:/jba/tools/sonar-scanner-4.3.0.2102/bin/sonar-scanner.bat -D sonar.projectKey=java-maven-junit-helloworld -D sonar.exclusions=**/src/**/*.java'
                }
            }
        }
        
    }
}
