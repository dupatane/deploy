pipeline{
    agent any
    stages{
      //git checkout private repo credentials are given in pipeline with scm //       
       stage('Build Stage'){
            steps{
                sh 'mvn clean install'
            }
         }
        stage('SonarQube Analysis Stage') {
            steps{
                withSonarQubeEnv('sonar') { 
                    sh "mvn clean verify sonar:sonar -Dsonar.projectKey=deploy"
                }
            }
        }
        stage('deploy to tomcat'){
             steps{
                echo 'this step to deploy artifact to tomcat environment'
           sh 'sudo cp /var/lib/jenkins/workspace/deploy/target/MyWebApp.war /opt/tomcat/apache-tomcat-9.0.68/webapps/'
             }
          } 

    }
    post {
        always {
            emailext attachLog: true, 
                     body: "hi,\nplease find the status of the job with following attachment:\n\nBuild Status: ${currentBuild.currentResult}\nConsole Output: ${BUILD_URL}console\n\nthanking you,\nkrishna dupatane", 
                     subject: "Build ${currentBuild.currentResult}: Job '${env.JOB_NAME} [${env.BUILD_NUMBER}]'", 
                     to: "dupatanekrishna@gmail.com"
        }
    }

}
