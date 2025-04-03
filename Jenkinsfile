pipeline {
    agent any

    stages {
        stage("Checkout code") {
            //checkout the repository
            steps {
                git branch: 'main', url: 'https://github.com/Ayrola/JenkinsDemo22'
            }
        }

        stage("Restoring nuget packages") {
            //checkout the repository
            steps {
                bat 'dotnet restore SeleniumIde.sln'
            }
        }

        stage("Build") {
            //checkout the repository
            steps {
                bat 'dotnet build SeleniumIde.sln --configuration Release'
            }
        }

        stage("Run Tests") {
            //checkout the repository
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