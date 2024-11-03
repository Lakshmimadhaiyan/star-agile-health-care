pipeline {
  agent any
     tools {
       maven 'M2_HOME'
           }
     
  stages {
    stage('Git Checkout') {
      steps {
        echo 'This stage is to clone the repo from github'
        git branch: 'master', url: 'https://github.com/Lakshmimadhaiyan/star-agile-health-care'
                        }
            }
    stage('Create Package') {
      steps {
        echo 'This stage will compile, test, package my application'
        sh 'mvn package'
                          }
            }
    stage('Generate Test Report') {
      steps {
        echo 'This stage generate Test report using TestNG'
        publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '/var/lib/jenkins/workspace/Healthcare/target/surefire-reports', reportFiles: 'index.html', reportName: 'HTML Report', reportTitles: '', useWrapperFileDirectly: true])
                          }
            }
    stage('Create Docker Image') {
      steps {
        echo 'This stage will Create a Docker image'
        sh 'docker build -t lalucky/healthcare:1.0 .'
                          }
            }
    stage('Login to Dockerhub') {
      steps {
        echo 'This stage will Create a Docker image'
        withCredentials([usernamePassword(credentialsId: 'Dockerlogin', passwordVariable: 'docker-pass', usernameVariable: 'docker-login')]) {
        sh 'docker login -u ${dockeruser} -p ${dockerpass}'
                                 }
      }
             }
       stage('Docker Push-Image') {
      steps {
        echo 'This stage will push my new image to the dockerhub'
        sh 'docker push lalucky/healthcare:1.0'
            }
      }
}
}
