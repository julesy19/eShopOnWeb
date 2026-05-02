pipeline {
  agent any
  stages {
    stage('Build') {
      steps {
        sh 'export PATH=$PATH:/root/.dotnet && dotnet build eShopOnWeb.sln'
      }
    }

    stage('Tests') {
      parallel {
        stage('Unit') {
          steps {
            sh 'dotnet test tests/UnitTests --no-build'
          }
        }

        stage('Integration') {
          steps {
            sh 'dotnet test tests/IntegrationTests --no-build'
          }
        }

        stage('Functional') {
          steps {
            sh 'dotnet test tests/FunctionalTests --no-build'
          }
        }

      }
    }

    stage('Deployment') {
      steps {
        sh 'dotnet publish src/Web/Web.csproj -c Release -o publish'
      }
    }

  }
}