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
                        "C:\\Program Files\\Snowflake SnowSQL\\snowsql.exe" -a xq67314.ap-southeast-7.aws ^
                                -u jenkins_svc ^
                                --private-key-path %SF_KEY_PATH% ^
                                -r JENKINS_ROLE ^
                                -w COMPUTE_WH ^
                                -d DEV_EDC_CON_DB ^
                                -s SALESFORCE ^
                                -f scripts\\deploy.sql
                    """
                }
            }
        }
    }
}
