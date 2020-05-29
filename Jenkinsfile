pipeline{
    
  agent { label "kubepod" }

  tools {
    maven "Maven-3.6.3"
  }
  
  stages {

  stage("Git Clone"){
    steps {
      git url: 'https://github.com/radek5/spring-boot-mongo-docker.git'
      }
    }
  }
}
