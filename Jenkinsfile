pipeline {
    agent any

    parameters {
        choice(choices: 'dev\ntest\ndemo\nproduction', description: '', name: 'env')
        string(name: 'App Version', defaultValue: '1.0.0', description: 'App version To Depoy')
    }
    
    stages {
        stage('Build') {
            steps { echo 'Building..' }
        }
        stage('Dev') {
            when { expression { params.env == 'dev' } }
            steps { echo 'Testing..' }
        }
        stage('Test Approval') {
            steps { def response = input(message: 'Deploy to Test?', ok: 'Yes', 
                        parameters: [booleanParam(defaultValue: true, 
                        description: 'If you like Java, just push the button',name: 'Yes?')]) }
        }
        stage('Test') {
            when { expression { params.env == 'test' } }
            steps {  echo 'Deploying....' }
        }
        stage('Approval') {
            steps { input 'Deploy to Production?' }
        }
        stage('Demo') {
            when { expression { params.env == 'Demo' } }
            steps { echo 'Deploying....' }
        }
        stage('Approval') {
            steps { input 'Deploy to Production?' }
        }
        stage('Production') {
             when { expression { params.env == 'production' } }
             steps {  echo 'Deploying....' }     
         }        
    }
}
