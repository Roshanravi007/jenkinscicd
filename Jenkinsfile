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