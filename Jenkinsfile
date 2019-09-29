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
            
           stage('Sonarqube') {
  
    steps {
            sh '/opt/maven/bin/mvn sonar:sonar'
        
    }
}
            
          
       
    }
}
