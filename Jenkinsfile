pipeline {
environment {
def dockerHome = tool 'mydocker'
env.PATH = "${dockerHome}/bin:${env.PATH}"  
registry = "arundhwaj/jenkins-test"
registryCredential = 'mydockerhub'
dockerImage = ''
}
agent any
stages {
stage('Cloning our Git') {
steps {
git 'https://github.com/ArunDhwaj/jenkins-test/'
}
}
stage('Building our image') {
steps{
script {
dockerImage = docker.build registry + ":$BUILD_NUMBER"
}
}
}
stage('Deploy our image') {
steps{
script {
docker.withRegistry( '', mydockerhub ) {
dockerImage.push()
}
}
}
}
stage('Cleaning up') {
steps{
sh "docker rmi $registry:$BUILD_NUMBER"
}
}
}
}
