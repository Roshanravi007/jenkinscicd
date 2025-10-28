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
   dir("target/"){
    stash name: "mvn-build", includes: "*.war"
   }
  }
  }
  }
}