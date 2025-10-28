pipeline 
{
  agent {
   label 'server1'
  }
  stage('build') {
   steps {
    sh 'mvn clean package -DskipTests=true'
   }
  }
  stage('test') {
   steps {
    sh 'mvn test'
   }
  }
}