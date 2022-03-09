pipeline {
    agent {
        docker {
            image 'maven:3.8.1-adoptopenjdk-11'
            args '-v /root/.m2:/root/.m2'
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
    }
}



sudo docker run \
  -u root \
  -d \
  --name jenkins \
  --restart always \
  -p 8080:8081 \
  -p 50000:50001 \
  -v /data/jenkins:/var/jenkins_home \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -e 'JENKINS_OPTS="--prefix=/jenkins"' \
  jenkinsci/blueocean