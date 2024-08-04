pipeline {
    agent any

    stages {
        stage("Checkout code") {
            // checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/EvgeniSimeonov/JenkinsSeleniumIdeDemoRepo_04_08'
            }
        }
        stage("Set up .Net Core") {
            // install dot net
        }
        stage("Restore dependencies") {
            // install dependencies
        }
        stage("Build") {
            // build
        }
        stage("Run Tests") {
            // run tests   
        }
    }
}