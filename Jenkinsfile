#!/usr/bin/env groovy

String IMAGE_NAME = 'dmp/sample-dmp'
String REGISTRY = 'dev-docker-registry.tecnotree.com'
String REGISTRY_URL = 'https://dev-docker-registry.tecnotree.com'
String REGISTRY_LOGIN = 'dev-docker-registry-login'
String BUILD_NUMBER = "${env.BUILD_NUMBER}"
String TAG="build-${BUILD_NUMBER}"


//Deployment variables
String devserverip = "172.20.23.87"
String testserverip = "172.20.23.87"

node('java-8-node'){
 
  try{
	
	stage('SCM') {
	 	// Checkout the commit that triggered the build
	  	git branch: 'master', credentialsId: 'generic-ssh-key-login', url: 'git@git.tecnotree.com:dmp/Digital_Market_Place-BE.git'
	  	}

	stage('Build') {
	 	// Install and run tests
		echo 'Build Stage'
		withMaven(maven: 'Maven 3.3.9') {
			def mvnHome = tool 'Maven 3.3.9'  
			sh 'mvn clean package'
			// Stash artifacts for docker packaging
			echo 'stashing dockerfile'
			stash name: "dockerfile", includes: "Dockerfile"
			echo 'stashing warfile'
			stash name: "warfile", includes: "target/jsp-boot-tst-1.0-SNAPSHOT.war"
		}
   	}
    		
}
 
  	catch (e) {
		currentBuild.result = "FAILED"
		throw e
  	}
}	

node('docker-node'){
	
	stage('Package'){
	    // Build docker image and push to repo
		docker.withRegistry(REGISTRY_URL, REGISTRY_LOGIN){
			deleteDir()
			echo 'Unstashing sources'
			unstash "dockerfile"
			unstash "warfile"
			sh 'ls -lrt'
			def snapshotImage = docker.build("${IMAGE_NAME}:${TAG}")
			sh 'docker login --username raghaar --password-stdin devops@21'
			snapshotImage.push(TAG)
			
			}
	}
}
		

