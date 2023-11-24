pipeline {
    agent any

    stages {
        stage('Hello') {
            steps {
                echo 'Hello World'
            }
        }
        stage('Checkout Project Test'){
            steps{
                checkout([$class: 'GitSCM',
                          branches: [[name: "main"]],
                          doGenerateSubmoduleConfigurations: false,
                          extensions: [],
                          gitTool: 'Default',
                          submoduleCfg: [],
                          userRemoteConfigs: [[credentialsId: 'Git-SSH-Credentials', url: "git@github.com:Axity-DieGom/Test.git"]]
                        ])
            }
        }
        stage('SonarQube Analysis') {
            def scannerHome = tool 'sonarqube';
            withSonarQubeEnv('sonarqube') {
                sh "${sonarqube}/bin/sonar-scanner \
                -Dsonar.projectKey=Test \ 
                -Dsonar.projectName=Test"
            }
        }
    }
}
