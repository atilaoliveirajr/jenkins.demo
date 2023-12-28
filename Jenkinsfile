pipeline {
    agent any

    stages {
        stage('checkout') {
            steps {
                echo "Scripts:"
                sh "ls"
                git branch: 'master', url: 'https://github.com/atilaoliveirajr/jenkins.demo.git'
                sh "ls"
            }
        }
        stage('build') {
            steps {
                sh "./mvnw package"
            }
        }
        stage('test') {
            parallel {
                stage('testA') {
                    steps {
                        echo "test set A"
                        sh "sleep 2"
                        sh "sleep 3"
                    }
                }
                stage('testB') {
                    steps {
                        echo "test set B"
                        sh "sleep 4"
                    }
                }
            }
        }
        stage('capture') {
            steps {
                archiveArtifacts '**/target/*.jar'
                jacoco()
                junit '**/target/surefire-reports/TEST*.xml'
            }
        }
    }
    
    post {
        always {
            echo "This is a test message in the post stage."
        }
    }
}