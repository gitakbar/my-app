node{
stage ('gitfetch') {
git  url:'https://github.com/gitakbar/my-app.git'
}
stage('mvn package'){
def mvnhome=tool name :'mymaven', type:'maven'
def mvncmd="${mvnhome}/bin/mvn"
sh "${mvncmd} clean package"
}
stage('build docker'){
sh 'docker build -t arahman009/dockerj . '
}
stage ('push docke image') {
withCredentials([string(credentialsId:'dockerhub',variable:'dockerhubpwd')]) {
sh "docker login -u arahman009 -p ${dockerhubpwd}"
}
sh 'docker push arahman009/dockerj:latest'
}
stage('run container on docker engin') {
def dockerrun='docker run -p 8080:8080 -d -name my-app arahman009/dockerj:latest'
sshagent(['dev-server']) {
sh "ssh -o StrictHostKeyChecking=no ec2-user@172.31.28.124 ${dockerrun}"
}
}
}
