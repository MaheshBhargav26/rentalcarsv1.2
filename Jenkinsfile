imagename = "061200616923.dkr.ecr.us-east-1.amazonaws.com/rentalcars"
ecrRegistry="https://061200616923.dkr.ecr.us-east-1.amazonaws.com/rentalcars"
awscreds = 'ecr:us-east-1:aws-creds'
node(){
stage("Git checkout"){
checkout scmGit(branches: [[name: '*/master']], extensions: [], userRemoteConfigs: [[url: 'https://github.com/MaheshBhargav26/rentalcarsv1.2.git']])

stage("Maven build"){
sh "mvn package"
}

stage("Build docker image"){
dockerImage = docker.build( imagename + ":$BUILD_NUMBER")

}

stage("Push docker image to ECR"){
                docker.withRegistry( ecrRegistry, awscreds) {
                dockerImage.push("$BUILD_NUMBER")
                dockerImage.push('latest')
              }
}
}