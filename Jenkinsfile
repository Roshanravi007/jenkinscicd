pipeline 
{
  agent {
   label 'server1'
  }
  parameters {
  choice choices: ['dev', 'prod'], name: 'select_environment'
  }
  stages {
   stage('build') {
    steps {
     sh 'mvn clean package -DskipTests=true'
    }
   }
   stage('test') {
    parallel {
     stage('testA') {
      steps {
       sh 'mvn test'
       echo 'I am from testA'
      }
     }
     stage('testB') {
      steps {
       sh 'mvn test'
       echo 'I am from testB'
      }
     }
    }
    post {
     success {
      dir('webapp/target/'){
      stash name: 'maven-build', includes: '*.war'
      }
     }
    }
   }
 
   stage('deploy'){
    when{
      expression {params.select_environment == 'dev'}
      beforeAgent true
    }
    agent{
      label 'server1'
    }
    steps {
      dir('/var/www/html'){
        unstash 'maven-build'
      }
      sh """
      cd /var/www/html
      jar -xvf webapp.war
      """
    }
   }
  }
}