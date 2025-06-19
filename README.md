pipeline {
    agent any
    
    environment {
        FORGE_EMAIL = credentials('FORGE_EMAIL')
        FORGE_API_TOKEN = credentials('FORGE_API_TOKEN')
    }
    
    stages {
        
        stage('Deploy Forge App') {
            steps {
                bat 'forge deploy --environment development'
            }
        }

        stage('Install Forge App') {
            steps {
                bat 'forge install --upgrade --site maxatn72.atlassian.net --product jira --non-interactive --environment development'
            }
        }
    }
}
