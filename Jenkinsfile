pipeline {
   agent any

   stages {
      stage('package') {
         steps {
            git 'https://github.com/vicziani/jenkins-demo'

            // Linux eset�n bat helyett sh az el�tag	    
            bat "mvnw -DskipTests clean package"	
         }
      }
      stage('test') {
         steps {
            bat "mvnw test"
         }
      }
      stage('deploy') {
         steps {
            bat "deploy.bat"
         }
      }
   }
}