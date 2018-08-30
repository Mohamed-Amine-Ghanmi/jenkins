pipeline {
    agent any

    parameters {
        string(name: 'Greeting', defaultValue: 'Hello', description: 'How should I greet the world?')
    }
    
    parameters {
        choice(
            // choices are a string of newline separated values
            // https://issues.jenkins-ci.org/browse/JENKINS-41180
            choices: 'dev\ntest\ndemo\nproduction',
            description: '',
            name: 'env')
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
            steps {
                timeout(time: 1, unit: 'MINUTES') {
                    input 'Deploy to Production?'
                }
            }     
        }
        
    }
}
