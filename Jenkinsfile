pipeline {
    agent any
    triggers { pollSCM('H/5 * * * *') }
    stages {
        stage('Build') {
            steps {
                echo '===== STAGE 1: BUILD ====='
                echo 'Tool: Maven'
                echo 'Task: Compile and package the code using Maven.'
                echo 'Command: mvn clean package'
            }
        }
        stage('Unit and Integration Tests') {
            steps {
                echo '===== STAGE 2: UNIT AND INTEGRATION TESTS ====='
                echo 'Tool: JUnit (Unit Tests), Selenium (Integration Tests)'
                echo 'Task: Run unit and integration tests to verify the application.'
                echo 'Command: mvn test'
            }
        }
        stage('Code Analysis') {
            steps {
                echo '===== STAGE 3: CODE ANALYSIS ====='
                echo 'Tool: SonarQube'
                echo 'Task: Analyse code quality and ensure industry standards are met.'
                echo 'Command: mvn sonar:sonar'
            }
        }
        stage('Security Scan') {
            steps {
                echo '===== STAGE 4: SECURITY SCAN ====='
                echo 'Tool: OWASP Dependency-Check'
                echo 'Task: Scan dependencies for known CVEs and vulnerabilities.'
                echo 'Command: mvn org.owasp:dependency-check-maven:check'
            }
        }
        stage('Deploy to Staging') {
            steps {
                echo '===== STAGE 5: DEPLOY TO STAGING ====='
                echo 'Tool: AWS CLI / SSH'
                echo 'Task: Deploy the application to an AWS EC2 staging instance.'
                echo 'Command: scp target/app.jar ec2-user@staging-server:/opt/app/'
            }
        }
        stage('Integration Tests on Staging') {
            steps {
                echo '===== STAGE 6: INTEGRATION TESTS ON STAGING ====='
                echo 'Tool: Postman / Newman CLI'
                echo 'Task: Run end-to-end tests on the staging environment.'
                echo 'Command: newman run collection.json --environment staging.json'
            }
        }
        stage('Deploy to Production') {
            steps {
                echo '===== STAGE 7: DEPLOY TO PRODUCTION ====='
                echo 'Tool: AWS CLI / SSH'
                echo 'Task: Deploy the verified application to the live production server.'
                echo 'Command: scp target/app.jar ec2-user@prod-server:/opt/app/'
            }
        }
    }
    post {
        success { echo 'All 7 stages passed successfully!' }
        failure { echo 'Pipeline failed. Check console output.' }
    }
}
