pipeline {
    agent any

    parameters {
        choice(
            // choices are a string of newline separated values
            // https://issues.jenkins-ci.org/browse/JENKINS-41180
            choices: 'dev\ntest\ndemo\nproduction',
            description: '',
            name: 'env')
        string(name: 'App Version', defaultValue: '1.0.0', description: 'App version To Depoy')
    }
    
    stages {
        stage('Example') {
            when {
                // Only say hello if a "greeting" is requested
                expression { params.env == 'dev' }
            }
            steps {
                echo "${params.Greeting} World!"
            }
        }
        stage('Build') {
            steps {
                echo 'Building..'
            }
        }
        stage('Dev') {
            when {
                // Only say hello if a "greeting" is requested
                expression { params.env == 'dev' }
            }
            steps {
                echo 'Testing..'
            }
        }
        stage('Test') {
            when {
                // Only say hello if a "greeting" is requested
                expression { params.env == 'test' }
            }
            steps {
                echo 'Deploying....'
            }
        }
        stage('Demo') {
            when {
                // Only say hello if a "greeting" is requested
                expression { params.env == 'Demo' }
            }
            steps {
                echo 'Deploying....'
            }
        }
        stage('Production') {
            when {
                // Only say hello if a "greeting" is requested
                expression { params.env == 'production' }
            }
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    input 'Deploy to Production?'
                }
            }     
        }
        
    }
}
