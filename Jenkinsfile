pipeline {
    agent { label 'new' }
    stages {
        stage('build') {
            steps {
                script {
                    if ( env.BRANCH_NAME == "deployment" || env.BRANCH_NAME == "development"  ) {
                    withCredentials([usernamePassword(credentialsId: "dockerhub" , usernameVariable: 'USER' , passwordVariable: 'PASS')]){
                        sh """
                            docker login -u ${USER} -p ${PASS}
                            docker build -t ahmedmongey/botit-image:${BUILD_NUMBER} .
                            docker push ahmedmongey/botit-image:${BUILD_NUMBER}
                            echo ${BUILD_NUMBER} > ../build.txt
                           """
                    }
                    }
                }
            }
        }
        
    }
}
