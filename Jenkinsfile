pipeline{
agent any
stages {
   stage('Pull code from GIT') {
      steps{
                checkout scm
      }
   }
   stage('Push Templates & Parameter files to S3') {
      steps{
      sh 'aws s3 cp ./JenkinsTemplate.yml s3://idexcel-interns-devops/'
      sh 'aws s3 cp ./Jenkinsfile s3://idexcel-interns-devops/'
      sh 'aws s3 cp ./Templates/Nested/ecs-cluster.yml s3://idexcel-interns-devops/Templates/Nested/ecs-cluster.yml'
      sh 'aws s3 cp ./Templates/Nested/ecs-service.yml s3://idexcel-interns-devops/Templates/Nested/ecs-service.yml'
      sh 'aws s3 cp ./Templates/${Stack}.yml s3://idexcel-interns-devops/Templates/${Stack}.yml'
      sh 'aws s3 cp ./Parameters/${EnvironmentType}/${Stack}.json s3://idexcel-interns-devops/Parameters/${EnvironmentType}/${Stack}.json'
      }
   }
   stage('Stack Action'){
      steps{
         sh 'aws --region us-east-1 cloudformation ${Action}-stack --stack-name ${EnvironmentType}-${Stack} --template-body file://./Templates/${Stack}.yml --parameters file://./Parameters/${EnvironmentType}/${Stack}.json'
      }
     }
   
   stage('Stack Status'){
      steps{
         sh 'aws --region us-east-1 cloudformation wait stack-${Action}-complete --stack-name ${EnvironmentType}-${Stack}'
      }
   }
}
post {
        always {
            echo 'Sending email notification....'
            
            emailext subject: "Jenkins Build ${currentBuild.currentResult}: Job ${env.JOB_NAME}"
                body: "${currentBuild.currentResult}: Job ${env.JOB_NAME} build ${env.BUILD_NUMBER}\n More info at: ${env.BUILD_URL}",
                from: "idexcel.interns@gmail.com",
                to: "sai.kanchana93@gmail.com"
                
            
        }
    }
}
