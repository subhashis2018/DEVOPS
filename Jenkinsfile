pipeline {
    agent any

    tools {
        maven 'Maven 3.9.6' // Adjust the Maven version as per your installation
        jdk 'jdk-17' // Adjust the JDK version as per your installation
    }

    environment {
        SONARQUBE_SERVER = 'SonarQube Server' // Name of the SonarQube server configured in Jenkins
        SPRINGBOOT_REPO = 'https://github.com/subhashis2018/springboot_cicd_1.git'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: "${SPRINGBOOT_REPO}"
            }
        }

        stage('Maven Clean') {
            steps {
                sh 'mvn clean'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn package'
            }
        }

        stage('SonarQube Analysis') {
            environment {
                scannerHome = tool 'SonarQube Scanner' // Adjust the tool name as per your configuration
            }
            steps {
                withSonarQubeEnv('SonarQube Server') { // Adjust the server name as per your configuration
                    sh "${scannerHome}/bin/sonar-scanner"
                }
            }
        }

        stage('Jacoco Code Coverage') {
            steps {
                sh 'mvn jacoco:report'
            }
        }

        stage('PMD Analysis') {
            steps {
                sh 'mvn pmd:pmd'
            }
        }

        stage('Publish Reports') {
            steps {
                jacoco execPattern: '**/target/*.exec', classPattern: '**/target/classes', sourcePattern: '**/src/main/java'
                pmd canComputeNew: false, pattern: '**/target/pmd.xml'
            }
        }
    }

    post {
        always {
            junit '**/target/surefire-reports/*.xml'
        }
    }
}
