pipeline {
    agent any
    stages {
        stage('Checkout'){
            steps{
                git branch: 'master', url: 'https://github.com/askrag93/test1.git'
            }
        }
        stage('Build') {
            steps{
                echo 'Build Stage'
                withMaven(maven: 'Maven-3.3.9') {
                    dir('C:\\Program Files (x86)\\Jenkins\\workspace\\sample'){
                    	
                        bat 'mvn -o clean install -Dmaven.test.skip=true'
                    }
                 }
     		 }
  	  }
        
        stage('War_Build') {
            steps{
                echo 'Build Stage'
                withMaven(maven: 'Maven-3.3.9') {
                    dir('C:\\Program Files (x86)\\Jenkins\\workspace\\sample\\EAR-COMMON'){
                    	
                        bat 'mvn -o clean install -Dmaven.test.skip=true'
                    }
                 }
     		 }
  	  }
     }
}


 
