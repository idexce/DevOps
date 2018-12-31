node {
   stage('Pull code from GIT') {
                checkout scm
   }
   stage('Stack Action'){
         sh 'aws cloudformation ${Action} --stack-name ${EnvironmentType}_${Stack} --template-body ./Templates/${Stack}.yml --parameters ./Parameters/${EnvironmentType}/${Stack}.json'
   }
}
