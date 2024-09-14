pipeline {
    agent any
    stages{
        stage('Build Maven'){
            steps{
                git url:'https://github.com/BasaveshRS/star-agile-health-care/', branch: "master"
               sh 'mvn clean package'
            }
        }
        stage('Build docker image'){
            steps{
                script{
                    sh 'docker build -t basaveshrs21/healthcareendtoendproject3:v1 .'
					sh 'docker images'
                }
            }
        }
          stage('Docker login') {
            steps {
                withCredentials([usernamePassword(credentialsId: 'dockerhub-pwd', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $PASS | docker login -u $USER --password-stdin"
                    sh 'docker push basaveshrs21/healthcareendtoendproject3:v1'
                }
            }
        }
        
        
        stage('Deploy'){
            steps{
                sh 'sudo docker run -itd --name My-first-containe1409 -p 8083:8081 basaveshrs21/healthcareendtoendproject3:v1'
                   
                }
            }
        
    }
}
