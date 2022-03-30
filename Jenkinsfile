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

        stage('Run') {
            steps {
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









        stage('transferFile'){
            steps{

                sshPublisher(
                        continueOnError: false, failOnError: true,
                        publishers: [
                                sshPublisherDesc(
                                        configName: "rouseaauNicolas",
                                        verbose: true,
                                        transfers: [
                                                sshTransfer(
                                                        sourceFiles: "*.html",
                                                        remoteDirectory: "/"
                                                ),
                                                sshTransfer(
                                                        sourceFiles: "out/movies/",
                                                        remoteDirectory: "/movies"
                                                )
                                        ])
                        ]
                )
            }
        }
















    }

}
//     post {
//         always {
//             junit '**/surefire-reports/*.xml'
//         }
//     }