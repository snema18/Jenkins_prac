pipeline{
    agent any
        stages{
   
           stage('Build'){
               steps{
git url: 'https://github.com/efsavage/hello-world-war.git'
             }
        }
       
        stage('Maven package'){
            steps{
       
            sh '/opt/maven/bin/mvn clean package'
        }
        }
             stage('sonar analysis'){
            steps{
       
           mvn sonar:sonar
        }
        }
        stage('Deploy the war file to tomcat container'){
            steps{
                deploy adapters: [tomcat9(credentialsId: '93ce2031-641d-4971-bab9-71912ee53dc6', path: '', url: 'http://13.233.89.152:8888/')], contextPath: 'demo', onFailure: false, war: '**/*.war'
            }
        }
    }
}
