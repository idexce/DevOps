node {
   stage('Pull code from GIT') {
                checkout scm
   }
   stage('Stack Action'){
         sh 'aws --region us-east-1 cloudformation ${Action} --stack-name ${EnvironmentType}_${Stack} --template-body ./Templates/${Stack}.yml --parameters file://./Parameters/${EnvironmentType}/${Stack}.json'
   }
}
