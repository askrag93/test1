pipeline {
    agent any
    stages {
        stage('Checkout'){
            steps{
                git branch: 'master', url: 'git@git.tecnotree.com:commerce-engine/CEngine.git'
            }
        }
        stage('Build') {
            steps{
                echo 'Build Stage'
                withMaven(maven: 'Maven-3.3.9') {
                    	sh 'pwd'
                        sh 'mvn clean install -Dmaven.test.skip=true'
                      }
     		 }
  	  }
     }
}


 
