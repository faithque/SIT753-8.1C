pipeline {
    agent any

    triggers {
        pollSCM('H/5 * * * *')  // Poll GitHub every 5 minutes
    }

    environment {
        STAGING_SERVER = 'ec2-user@your-staging-ec2-ip'
        PROD_SERVER = 'ec2-user@your-production-ec2-ip'
    }

    stages {
        stage('Build') {
            steps {
                echo 'Building the application...'
                echo 'Description: This stage builds the application using Maven.'
                //sh 'mvn clean package'
            }
        }

        stage('Unit and Integration Tests') {
            steps {
                echo 'Running unit and integration tests...'
                echo 'Description: This stage runs unit tests and integration tests using JUnit.'
                //sh 'mvn test'
            }
        }

        stage('Code Analysis') {
            steps {
                echo 'Performing code analysis with SonarQube...'
                echo 'Description: This stage performs static code analysis using SonarQube.'
                // Assumes SonarQube plugin is configured in Jenkins
                //sh 'mvn sonar:sonar -Dsonar.projectKey=SIT753-8.1C -Dsonar.host.url=http://your-sonarqube-url'
            }
        }

        stage('Security Scan') {
            steps {
                echo 'Running security scan with OWASP Dependency-Check...'
                echo 'Description: This stage scans for vulnerabilities in dependencies using OWASP Dependency-Check.'
                // Assumes OWASP Dependency-Check is installed and configured in Jenkins
                //sh './dependency-check/bin/dependency-check.sh --project MyProject --scan .'
            }
        }

        stage('Deploy to Staging') {
            when {
              expression {
                currentBuild.result == null || currentBuild.result == 'SUCCESS' 
              }
            }
            steps {
                echo 'Deploying to staging server...'
                echo 'Description: This stage deploys the application to the staging server.'
                //sh 'ssh $STAGING_SERVER "java -jar /home/ec2-user/app/myapp.jar &"'
            }
        }

        stage('Integration Tests on Staging') {
            steps {
                echo 'Running integration tests on staging environment...'
                echo 'Description: This stage runs integration tests on the staging environment using Postman/Newman.'
                // Assumes Postman/Newman is installed and configured in Jenkins
                //sh 'newman run my-postman-collection.json --env-var "url=http://your-staging-url"'
            }
        }

        stage('Deploy to Production') {
            steps {
                input message: 'Approve deployment to production?'
                echo 'Deploying to production server...'
                echo 'Description: This stage deploys the application to the production server.'
                //sh 'ssh $PROD_SERVER "pkill -f myapp.jar || true; java -jar /home/ec2-user/app/myapp.jar &"'
            }
        }
    }
}