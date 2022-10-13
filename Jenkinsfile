pipeline {
  agent any
  
  stages {
        stage('test') {
            steps {
            sh "echo The login user is ${USER}"
            }
        }
     

        stage('deployment') {
            environment { 
                SSH_CRED = credentials('jenkinstest-pem')
            }
            steps{         
                script {
                    sh """
                    #!/bin/bash
		            echo "connecting to remote or deploy server"	
                    ssh -i $SSH_CRED -t -o StrictHostKeyChecking=no ubuntu@ec2-3-97-8-155.ca-central-1.compute.amazonaws.com << EOF
                    sudo mkdir resume
                    cd resume
                    sudo git clone https://github.com/tolaoguntunde/Resume_Website.git .
                    cd ..
                    sudo mv resume /var/www/resume
                    echo "exiting terminal"
                    exit
                    << EOF
                    """
                }
            }
        }
    }
}
