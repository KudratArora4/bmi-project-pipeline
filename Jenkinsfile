pipeline {
    agent any

    environment {
        STAGING_ENV = 'AWS EC2'      // Staging environment --> example
        PRODUCTION_ENV = 'AWS EC2'  // Production environment --> example
        EMAIL = 'kudratskarora@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using npm install'
                //this stage installs dependencies and compiles the application
                //[Other Available Tools for various project types --> Maven, Gradle, yarn]
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using Jest'
                //this stage runs unit and integration tests to verify functionality and component interactions
                //[Other Available Tools for various project types -->  JUnit, TestNG, Mocha]
            }
            post {
                always {
                    emailext to: "${env.EMAIL}" ,
                             subject: "Unit and Integration Tests --> ${currentBuild.currentResult} - ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                             body: "The unit and integration tests for ${env.JOB_NAME} Build #${env.BUILD_NUMBER} completed with status --> ${currentBuild.currentResult}. Logs are attached",
                             attachLog: true
                }
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis using SonarQube'
                //this stage analyzes the code quality, checks for bugs, vulnerabilities and ensures compliance with standards
                //[Other Available Tools for various project types --> ESLint, Checkstyle]
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
                //this stage scans the application for security vulnerabilities and weaknesses
                //[Other Available Tools for various project types --> Snyk, Dependency-Check]
            }
            post {
                always {
                    emailext to: "${env.EMAIL}" ,
                             subject: "Security Scan --> ${currentBuild.currentResult} - ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                             body: "The security scan for ${env.JOB_NAME} Build #${env.BUILD_NUMBER} completed with status --> ${currentBuild.currentResult}. Logs are attached",
                             attachLog: true
                }
            }
        }

        stage('Deploy to Staging') {
            steps {
                echo "Deploying application to staging environment using ${env.STAGING_ENV} "
                //this stage deploys the application to a staging environment for further testing
                //[Other Available Tools for various project types --> Docker, Kubernetes]
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment using Cypress'
                //this stage tests the application in the staging environment to ensure it behaves as expected before production deployment
                //[Other Available Tools for various project types --> Selenium, Postman, JMeter]
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying application to production environment using ${env.PRODUCTION_ENV}"
                //this stage deploys the finalized application to the production environment
                //[Other Available Tools for various project types --> Docker, Kubernetes, Azure App Services]
            }
        }
    }

    post {
        always {
            emailext to: "${env.EMAIL}" ,
                     subject: "Jenkins Pipeline -->  ${currentBuild.currentResult} - ${env.JOB_NAME} Build #${env.BUILD_NUMBER}",
                     body: "The pipeline for ${env.JOB_NAME} Build #${env.BUILD_NUMBER} has completed with status --> ${currentBuild.currentResult}. Logs are attached",
                     attachLog: true
        }
    }
}
