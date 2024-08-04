pipeline {
    agent any

    stages {
        stage("Checkout code") {
            // checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/EvgeniSimeonov/JenkinsSeleniumIdeDemoRepo_04_08'
            }
        }
    }
}