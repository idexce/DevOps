node {
   stage('Pull code from GIT') {
                checkout scm
   }
   stage('Stack Action'){
         sh 'aws --region us-east-1 cloudformation ${Action} --stack-name ${EnvironmentType}-${Stack} --template-body file://./Templates/${Stack}.yml --parameters file://./Parameters/${EnvironmentType}/${Stack}.json'
   }
}
