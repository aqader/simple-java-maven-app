pipeline {
    agent any
    tools { 
        maven 'maven' 
        jdk 'jdk17' 
    }
    environment {
        REPO = 'matrix' // Artifactory repository
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
                    def server = Artifactory.server('mtx_jfrog') // Artifactory server ID in Jenkins
                    def uploadSpec = """{
                        "files": [{
                            "pattern": "target/*.jar", // Adjust to match your artifact
                            "target": "${REPO}/simple-java-maven-app/"
                        }]
                    }"""
                    server.upload(uploadSpec)
                }
            }
        }
    }
}
