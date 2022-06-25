pipeline {
    agent {
        docker {
            image 'mcr.microsoft.com/dotnet/aspnet:6.0'
        }
    }
    stages {
        stage('Verify') {
            steps {
                sh '''
                  dotnet --list-sdks
                  dotnet --list-runtimes
                '''
                sh 'printenv'
                sh 'ls -l "$WORKSPACE"'
            }
        }
        stage('Build') {
            steps {
                sh 'dotnet build "$WORKSPACE/src/web-api/web-api.csproj"'
            }
        }
        stage('API Unit Test') {
            steps {
              dir("$WORKSPACE/src") {
                sh '''
                    dotnet test web-api-tests/web-api-tests.csproj
                '''
              }
            }
        }
    }
}
