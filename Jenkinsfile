pipeline { 
  
   agent any

   stages {
   
     stage('Install Dependencies') {
        when {
            branch 'development'
        } 
        steps { 
           sh 'sudo yum install python3 pip3' 
           sh 'sudo pip3 install virtualenv '
           sh 'virtualenv my-project'
           sh 'python -m venv exvenv'
           sh 'source my-project/bin/activate' 
           sh 'pip install -r my-project/requirements.txt'
        }
     }
     
     stage('Test') { 
        when {
            branch 'development'
        }
        steps { 
           sh 'python ./tests/test_hello.py'
        }
      }

         stage("Deploy application") {
            when {
                branch 'deployment'
            } 
         steps { 
           sh 'python ./src/hello.py'
           sh 'sudo docker pull ahmedmongey/botit-image:v6'
           sh 'sudo docker build -t ahmedmongey/botit-image:v6 .'
           sh 'sudo docker run -itd -p 5000:5000 ahmedmongey/botit-image:v6 '
         }

     }
  
   	}

   }
