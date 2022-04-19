pipeline{
    agent any
    stages{
        stage('code_ceckout'){
          steps{
            checkout([$class: 'GitSCM', branches: [[name: '*/main']], extensions: [], userRemoteConfigs: [[credentialsId: 'git_cred', url: 'https://github.com/subhash69/sample_maven_project.git']]])  
          }
        }
        stage('maven_build'){
            steps{
                sh "mvn clean install"
            }
        }
        stage('deploy_tomcat'){
            steps{
               sshagent(['tomcat_server']) {
                 sh "scp -r /var/lib/jenkins/workspace/demo-tomcat/target/*.war lamadmin@13.76.242.73:/opt/tomcat/webapps"
                } 
            }
        }
    }
}
