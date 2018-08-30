#!/bin/groovy
def userInput

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
            when { expression { params.env == 'dev' } }
            steps {
                script {
                   userInput = input(id: 'userInput', message: 'Merge to Test?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'TestChoice', choices: "skip-Next\ntest\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Test') {
            when { expression { params.env == 'test' || userInput == 'test' } }
            steps {  echo 'Deploying....' }
        }
        stage('Demo Approval') {
            when { expression { params.env == 'test' || userInput == 'test' } }
            steps {
                script {
                   userInput = input(id: 'userInput', message: 'Merge to Demo ?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'DemoChoice', choices: "skip-Next\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Demo') {
            when { expression { params.env == 'demo' || userInput == 'demo' } }
            steps { echo 'Deploying....' }
        }
        stage('Approval') {
            when { expression { params.env == 'demo' || userInput == 'demo' } }
            steps {
                script {
                   userInput = input(id: 'userInput', message: 'Merge to Production ?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'Choice', choices: "skip-Next\nproduction"]
                    ])
                 }
            }
        }
        stage('Production') {
             when { expression { params.env == 'production' || userInput == 'production' } }
             steps {  echo 'Deploying....' }     
         }        
    }
}
