pipeline {
    agent any

    parameters {
        choice(choices: 'dev\ntest\ndemo\nproduction', description: '', name: 'env')
        string(name: 'App Version', defaultValue: '1.0.0', description: 'App version To Depoy')
    }
    
    stages {
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
        stage('Approval') {
            steps {
                 input 'Deploy to Production?'
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
