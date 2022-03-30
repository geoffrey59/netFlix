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

    stage('Run'){
            steps{
                sh 'java -jar  ./target/netflix-1.0.0.jar  netflix_titles.csv'
                }
            }

    stage('Sonarqube') {
            steps {
               withSonarQubeEnv('sonarqube-scanner') {
                    sh "mvn verify sonar:sonar"
               }
            }
    }
}




//     post {
//         always {
//             junit '**/surefire-reports/*.xml'
//         }
//     }