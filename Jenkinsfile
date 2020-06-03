node{
    
stage("Git Clone"){
      git url: 'https://github.com/radek5/spring-boot-mongo-docker.git'
    } 
    
stage("Maven Clean Build"){
       echo mavenHome = tool name: "Maven-3.6.3", type: "maven"
       echo mavenCMD = "${mavenHome}/bin/mvn"
       sh "${mavenCMD} clean package"
    }
    
   stage("Build Docker Image"){
      sh "docker build -t 380987008477.dkr.ecr.eu-west-2.amazonaws.com/spring-boot-mongo ."
    }  
  }


