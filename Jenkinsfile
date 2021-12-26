node {
stage('SCM-Checkout'){
git 'https://github.com/gitakbar/my-app' }
stage ('compile-package')
{ def mvnhome=tool name:'maven2',type: 'maven'
sh "${mvnhome}/bin/mvn clean install package"
}
}
