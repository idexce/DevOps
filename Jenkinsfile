node {
   stage('Stack Action'){
         sh 'aws cloudformation ${Action} --stack-name ${EnvironmentType}_${Stack} --template-url https://github.com/idexcel-interns/DevOps/tree/master/Templates/${Stack}.yml --parameters https://github.com/idexcel-interns/DevOps/tree/master/Parameters/${EnvironmentType}/${Stack}.json'
   }
}
