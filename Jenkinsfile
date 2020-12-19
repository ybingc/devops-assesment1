pipeline {



  environment {

    registry = "ybingc/project1"

    registryCredential = 'dockerhub'

  }



  agent any

  stages {

        stage("Building image") {

        steps{

            script {

                 dockerImage = docker.build registry + ":$BUILD_NUMBER"

                 } 

              }

        }



        stage("Deploy image") {

        steps{

            script {

                 docker.withRegistry( '', 'dockerhub' ) {

                      dockerImage.push()

                      }

                 } 

              }

        }



        stage("Remove image") {

        steps{

            sh "docker rmi $registry:$BUILD_NUMBER" 

             }

        }

  }

}



node {

    stage('Execute Image') {

        def customImage = docker.build("ybingc/project1:${env.BUILD_NUMBER}")

        customImage.inside {

            sh 'echo This is the code executing inside the container.'

        }

    }



}

