pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11'
        }
    }
    stages {
        stage('Build') {
            steps {
                sh 'mvn -B -DskipTests clean package'
            }
        }
    stage ('prepare'){
            steps{
                git url:"https://github.com/geoffrey59/netFlix.git/",
                    branch: "test"
    }       }

    stage('Run'){
            steps{
                sh 'java -jar  ./target/netflix-1.0.0.jar  netflix_titles.csv'
                }
            }
    }

    post {
        always {
            junit '**/surefire-reports/*.xml'
        }
    }
}

