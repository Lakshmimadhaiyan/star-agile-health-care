pipeline {
  agent any
     tools {
       maven 'M2_HOME'
           }
       environment {
  AWS-ACCESS_KEY_ID - crendentials('aws-access-key-id')
  AWS_SECRET_ACCESS_KEY - credentials('aws-secret-access-key')
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
        echo 'This stage will create a Docker image'
        sh 'docker build -t laksm/healthcare:1.0 .'
    }
}

stage('Login to Dockerhub') {
    steps {
        echo 'This stage will Logging in to Docker Hub...'
        withCredentials([usernamePassword(credentialsId: 'dockerlogin', passwordVariable: 'dockerpass', usernameVariable: 'dockerlogin')]) {
        sh 'docker login -u $dockerlogin -p $dockerpass'
        }
    }
}
stage('Docker Push Image') {
    steps {
        echo 'This stage will Push the new image to Docker Hub...'
        sh 'docker push laksm/healthcare:1.0'
    }
                            }
}
}
