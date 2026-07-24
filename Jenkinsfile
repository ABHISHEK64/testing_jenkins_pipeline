pipeline {
    agent any
    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/ABHISHEK64/testing_jenkins_pipeline.git'
            }
        }
        stage('Run Snowflake SQL') {
            steps {
                withCredentials([file(credentialsId: 'snowflake-private-key', variable: 'SF_KEY_PATH')]) {
                    bat """
                        snowsql -a MK58698 ^
                                -u jenkins_svc ^
                                --private-key-path %SF_KEY_PATH% ^
                                -r JENKINS_ROLE ^
                                -w COMPUTE_WH ^
                                -d DEV_EDC_CON_DB ^
                                -s YOUR_SCHEMA_NAME ^
                                -f scripts\\deploy.sql
                    """
                }
            }
        }
    }
}
