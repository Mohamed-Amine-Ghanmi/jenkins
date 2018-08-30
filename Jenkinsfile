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
            steps {
                script {
                   def userInput = input(id: 'userInput', message: 'Merge to Test?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'TestChoice', choices: "test\ndemo\nproduction"]
                    ])
                 }
                echo '$userInput'
            }
        }
        stage('Test') {
            when { expression { params.env == 'test' || userInput['TestChoice'] == 'test' } }
            steps {  echo 'Deploying....' }
        }
        stage('Demo Approval') {
            steps {
                script {
                   def userInput = input(id: 'userInput', message: 'Merge to Demo ?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'DemoChoice', choices: "test\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Demo') {
            when { expression { params.env == 'Demo' || userInput['DemoChoice'] == 'demo' } }
            steps { echo 'Deploying....' }
        }
        stage('Approval') {
            steps {
                script {
                   def userInput = input(id: 'userInput', message: 'Merge to Production ?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'Choice', choices: "test\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Production') {
             when { expression { params.env == 'production' || userInput['Choice'] == 'production' } }
             steps {  echo 'Deploying....' }     
         }        
    }
}
