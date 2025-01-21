pipeline{
    agent{
        docker{
            image "node:lts-jod"
            args "-u root"
        }
    }
    environment{
        DIRECTORY = "/var/www/teacher_project_Sukhorukova"
        PROD_CRED_ID = "devops_prod_key"        
	    PROD_ADDRESS_CRED_ID = "devops_prod_address"  
    }
  stages{
    stage("Installing"){
      steps{
        sh "npm install"
      }
    }

    stage("Build"){
        steps{
            sh "npm run build_prod"
        }
    }

    stage("Production"){
        steps{
            withCredentials([sshUserPrivateKey(credentialsId: "${PROD_CRED_ID}", keyFileVariable: 'KEY_FILE', usernameVariable:'USERNAME'),                        
			string(credentialsId: "${PROD_ADDRESS_CRED_ID}", variable:'SERVER_ADDRESS')]){                                     
				sh 'scp -o StrictHostKeyChecking=no -i "${KEY_FILE}" dist ${USERNAME}@${SERVER_ADDRESS}:${DIRECTORY}'                    
			}   
        }
    }
  }
}
