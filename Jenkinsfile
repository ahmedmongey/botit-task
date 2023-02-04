pipeline {

    agent any

    stages{
        stage('Build') {
          steps {
            script {
              withCredentials([usernamePassword(credentialsId: 'DockerHub', usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD')]) { 

              sh """
                systemctl start docker
                docker build -t ahmedmongey/botit-image:V${BUILD_NUMBER} .
                echo ${BUILD_NUMBER}
                docker login -u ${USERNAME} -p ${PASSWORD}
                docker push ahmedmongey/botit-image:V${BUILD_NUMBER}
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
                              systemctl start docker
                              docker run -d -p 5000:5000 --name task omarkorety/botit:V${BUILD_NUMBER}
                            """
                }

              }
            
          }
        }

}
