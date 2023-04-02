pipeline{
    agent any
    stages{
      // stage('Git Checkout Stage'){
       //     steps{
       //         git branch: 'main', url: 'https://github.com/dupatane/deploy.git'
       //     }
      //   }        
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
    }
}
