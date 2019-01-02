node {
   stage('Pull code from GIT') {
                checkout scm
   }
   stage('Push Templates & Parameter files to S3') {
      sh 'aws s3 cp ./JenkinsTemplate.yml s3://idexcel-interns-devops/'
      sh 'aws s3 cp ./Templates/Nested/ecs-cluster.yml s3://idexcel-interns-devops/Templates/Nested/ecs-cluster.yml'
      sh 'aws s3 cp ./Templates/Nested/ecs-service.yml s3://idexcel-interns-devops/Templates/Nested/ecs-service.yml'
      sh 'aws s3 cp ./Templates/${Stack}.yml s3://idexcel-interns-devops/Templates/${Stack}.yml'
      sh 'aws s3 cp ./Parameters/${EnvironmentType}/${Stack}.json s3://idexcel-interns-devops/Parameters/${EnvironmentType}/${Stack}.json'
   }
   stage('Stack Action'){
         sh 'aws --region us-east-1 cloudformation ${Action} --stack-name ${EnvironmentType}-${Stack} --template-body file://./Templates/${Stack}.yml --parameters file://./Parameters/${EnvironmentType}/${Stack}.json'
   }
}
