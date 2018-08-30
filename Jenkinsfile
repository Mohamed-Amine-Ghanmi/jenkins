pipeline {
    agent any

    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    stages {
        stage('Example') {
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
            steps {
                echo 'Testing..'
            }
        }
        stage('Test') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Demo') {
            steps {
                echo 'Deploying....'
            }
        }
        stage('Production') {
            timeout(time: 1, unit: 'HOURS') {
                input 'Deploy to Production?'
            }
        }
        
    }
}
