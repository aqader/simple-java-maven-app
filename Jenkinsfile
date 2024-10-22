pipeline {
    agent any
    tools { 
        maven 'maven' 
        jdk 'jdk17' 
    }
    environment {
        REPO = 'matrix' 
    }
    stages {
        stage('Build') { 
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
        stage('Upload to Artifactory') {
            steps {
                script {
                    def server = Artifactory.server('mtx_jfrog') 
                    def uploadSpec = """{
                        "files": [{
                            "pattern": "target/*.jar", 
                            "target": "${REPO}/simple-java-maven-app/"
                        }]
                    }"""
                    server.upload(uploadSpec)
                }
            }
        }
    }
}
