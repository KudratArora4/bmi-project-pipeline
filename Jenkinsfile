pipeline {
    agent any

    environment {
        STAGING_ENV = 'AWS EC2'      //Staging environment --> example
        PRODUCTION_ENV = 'AWS EC2'  //Production environment --> example
        EMAIL = 'arorakudrat19@gmail.com'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application using npm install'
                //[Other Available Tools for various project types --> Maven, Gradle, yarn]
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests using Jest'
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
                  //[Other Available Tools for various project types --> ESLint, Checkstyle]
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Performing security scan using OWASP ZAP'
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
                //[Other Available Tools for various project types --> Docker, Kubernetes]
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment using Cypress'
                //[Other Available Tools for various project types --> Selenium, Postman, JMeter]
            }
        }

        stage('Deploy to Production') {
            steps {
                echo "Deploying application to production environment using ${env.PRODUCTION_ENV}"
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
