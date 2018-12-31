node {
   stage('Stack Action'){
         sh 'aws cloudformation ${Action} --stack-name ${EnvironmentType}_${Stack} --template-url https://github.com/idexcel-interns/DevOps/Templates/${Stack}.yml --parameters file://https://github.com/idexcel-interns/DevOps/Parameters/${EnvironmentType}/${Stack}.json'
   }
}
