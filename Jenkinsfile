pipeline {
    agent any

    stages {
        stage("Checkout code") {
            steps {
                git branch: 'main', url: 'https://github.com/EvgeniSimeonov/JenkinsSeleniumIdeDemoRepo_04_08'
            }
        }

        stage("Set up .Net Core and EdgeDriver") {
            steps {
                bat '''
                echo Downloading .Net 6 Sdk
                curl -L -o dotnet-sdk-6.0.132-win-x86.exe https://download.visualstudio.microsoft.com/download/pr/ad59f1d1-5f19-4474-86be-2f09ab195618/5c7a64445dae84e386bb88e1f6ac09e4/dotnet-sdk-6.0.132-win-x86.exe
                echo Installing dotnet-sdk-6.0.132-win-x86.exe
                start /wait dotnet-sdk-6.0.132-win-x86.exe /quiet /norestart
                echo Downloading EdgeDriver
                curl -L -o edgedriver_win64.zip https://msedgedriver.azureedge.net/XXX/edgedriver_win64.zip
                echo Unzipping EdgeDriver
                powershell -Command "Expand-Archive -Path edgedriver_win64.zip -DestinationPath ."
                set PATH=%PATH%;%cd%
                '''
            }
        }

        stage("Restoring nuget packages") {
            steps {
                bat 'dotnet restore SeleniumIde.sln'
            }
        }

        stage("Build") {
            steps {
                bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
        }

        stage("Run tests") {
            steps {
                bat 'dotnet test SeleniumIde.sln --logger "trx;LogFileName=TestResults.trx"'
            }
        }
    }

    post {
        always {
            archiveArtifacts artifacts: '**/TestResults/*.trx', allowEmptyArchive: true
            step([
                $class: 'MSTestPublisher',
                testResultsFile: '**/TestResults/*.trx'
            ])
        }
    }
}
