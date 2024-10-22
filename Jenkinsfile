pipeline {
    agent any
    tools { 
        maven 'maven' 
        jdk 'jdk17' 
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package' 
            }
        }
    }
}
