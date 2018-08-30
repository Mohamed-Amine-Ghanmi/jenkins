#!/bin/groovy
def userInput

pipeline {
    agent any
    
    parameters {
        choice(choices: 'dev\ntest\ndemo\nproduction', description: '', name: 'env')
        string(name: 'version', defaultValue: '1.0.0', description: 'App version To Depoy')
    }
    
    stages {
        stage('Build') {
            steps { echo 'Building..' }
        }
        stage('Dev') {
            when { expression { params.env == 'dev' } }
            steps { 
                echo 'Dev..'
                dir ('/tmp/Hello_world_Assignement') {
                    sh "./scripts/install_dependecies.sh"
                    sh "echo 'yes' | ./scripts/Build_Deploy_S3_Lambda_Apigw.sh ${params.env} ${params.version}"
                }
            }
        }
        stage('Test Approval') {
            when { expression { params.env == 'dev' } }
            steps {
                script {
                   userInput = input(id: 'userInput', message: 'Merge to Test?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'TestChoice', choices: "finish\ntest\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Test') {
            when { expression { params.env == 'test' || userInput == 'test' } }
            steps {  echo 'Test....' }
        }
        stage('Demo Approval') {
            when { expression { params.env == 'test' || userInput == 'test' } }
            steps {
                script {
                   userInput = input(id: 'userInput', message: 'Merge to Demo ?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'DemoChoice', choices: "finish\ndemo\nproduction"]
                    ])
                 }
            }
        }
        stage('Demo') {
            when { expression { params.env == 'demo' || userInput == 'demo' } }
            steps { echo 'Demo....' }
        }
        stage('Approval') {
            when { expression { params.env == 'demo' || userInput == 'demo' } }
            steps {
                script {
                   userInput = input(id: 'userInput', message: 'Merge to Production ?',
                   parameters: [[$class: 'ChoiceParameterDefinition', defaultValue: 'strDef', 
                       description:'describing choices', name:'Choice', choices: "finish\nproduction"]
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
