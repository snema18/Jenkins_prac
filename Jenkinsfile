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
        stage('Deploy the war file to tomcat container'){
            steps{
                deploy adapters: [tomcat9(credentialsId: '9814b801-6ff0-483c-975b-6e771a3e3be4', path: '', url: 'http://18.223.171.12:8090/')], contextPath: 'Hello-world-warr', war: '**/*.war'
            }
        }
    }
}
