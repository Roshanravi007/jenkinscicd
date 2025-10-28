pipeline 
{
  agent {
   label 'server1'
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
   }
  post {
   success {
    dir('webapp/target/'){
     stash name: 'maven-build', includes: '*.war'
    }
   }
  }
   stage('deploy'){
    steps {
      dir('var/www/html'){
        unstash 'maven-build'
      }
      sh 
      """
      cd /var/www/html
      jar -xvf webapp.war
      """
    }
   }
  }
}