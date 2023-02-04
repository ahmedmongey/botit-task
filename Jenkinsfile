pipeline {

    agent any

    stages{
        stage('Build') {
          steps {
            script {
              withCredentials([usernamePassword(credentialsId: 'DockerHub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) { 

              sh """
                sudo docker build -t ahmedmongey/botit-image:V${BUILD_NUMBER} .
                echo ${BUILD_NUMBER}
                sudo docker login -u ${USERNAME} -p ${PASSWORD}
                sudo docker push ahmedmongey/botit-image:V${BUILD_NUMBER}
                echo ${BUILD_NUMBER} > ../build_num.txt
                """
                    }
                        } 
                }
            }
    

        stage('Deploy') {
          steps{
            script {

                            sh """

                              sudo docker run -d -p 5000:5000 --name task omarkorety/botit:V${BUILD_NUMBER}
                            """
                }

              }
            
          }
        }

}
