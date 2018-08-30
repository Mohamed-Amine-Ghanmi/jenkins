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
                   def userInput1 = input(id: 'userInput1', message: 'Merge to Test?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'nameChoice', choices: "test\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Test') {
            when { expression { params.env == 'test' || userInput1 == 'test' } }
            steps {  echo 'Deploying....' }
        }
        stage('Demo Approval') {
            steps {
                script {
                   def userInput2 = input(id: 'userInput2', message: 'Merge to Demo ?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'nameChoice', choices: "test\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Demo') {
            when { expression { params.env == 'Demo' || userInput2 == 'demo' } }
            steps { echo 'Deploying....' }
        }
        stage('Approval') {
            steps {
                script {
                   def userInput3 = input(id: 'userInput3', message: 'Merge to Production ?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'nameChoice', choices: "test\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Production') {
             when { expression { params.env == 'production' || userInput3 == 'production' } }
             steps {  echo 'Deploying....' }     
         }        
    }
}
