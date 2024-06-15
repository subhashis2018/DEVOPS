pipeline {
    agent any

     tools {
        maven 'maven-3.9.6' // Adjust the Maven version as per your installation
        jdk 'jdk-17' // Adjust the JDK version as per your installation
     }

    environment {
        GIT_REPO_URL = 'https://github.com/subhashis2018/springboot_cicd_1.git'
        BRANCH_NAME = 'main'
    }

    stages {
        stage('Clone Repository') {
            steps {
                git branch: "${BRANCH_NAME}",
                    url: "${GIT_REPO_URL}",
                    credentialsId: 'your-credentials-id'
            }
        }
        stage('Maven Clean') {
            steps {
                // export JAVA_HOME=/usr/lib/jvm/jdk-17-oracle-x64
                // export MVN_HOME=/usr/share/maven
                // export PATH=$JAVA_HOME/bin:$MVN_HOME/bin:$PATH
                sh 'mvn clean'
            }
        }

        stage('Maven Build') {
            steps {
                sh 'mvn package'
            }
        }
        stage('Maven Test') {
            steps {
                sh 'mvn test'
            }
        }
    }

    post {
        success {
            echo 'Build completed successfully!'
        }
        failure {
            echo 'Build failed!'
        }
    }
}
