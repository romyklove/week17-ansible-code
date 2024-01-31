pipeline {
   agent any
      stages{
        stage('Zip the file and Push to Jfrog'){
           steps{
            script{
                // Create a zip file containing all files except Jenkinsfile
              sh 'zip -r code.zip * -x Jenkinsfile' 

               // Upload the zip file to JFrog Artifactory
               sh 'curl -uadmin:AP8FLm7718W6o5MZnPEHVRnaYwx -T code.zip "http://44.211.177.137:8081/artifactory/code/code.zip"'
            }
           
           }
        }
      stage('Download Artifact from Jfrog') {
         agent {
            label 'ansible2'
         }
         steps {
            script {
               // Download the zip file from Jfrog Artifactory
             sh 'curl -uadmin:AP8FLm7718W6o5MZnPEHVRnaYwx -O "http://44.211.177.137:8081/artifactory/code/code.zip"'
             // Now you can use the downloaded files on the agent
            }
         }
      }
      stage(' Run playbook') {
         agent {
            label 'ansible2'
         }
         steps{
             script{
                // Unzip code.zip
                    sh 'unzip -o code.zip'
                    // Run ansible-playbook from the correct directory
                    dir('code') {
                        
                        sh 'ansible-playbook -i /home/ec2-user/ansible1.dev/inventory.yml /home/ec2-user/ansible1.dev/play1.yml'
                 }
              }

           }   
        } 

   }
}

