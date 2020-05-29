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
   
   stage("Maven Clean Build"){
     steps {
       echo mavenHome = tool name: "Maven-3.6.3", type: "maven"
       echo mavenCMD = "${mavenHome}/bin/mvn"
       sh "${mavenCMD} clean package"
      }
    }
    
  stage("Build Docker Image"){
    steps {
      sh "docker build -t 380987008477.dkr.ecr.eu-west-2.amazonaws.com/spring-boot-mongo ."
    }
  }
    
  stage("Push Docker Image"){
    steps {
      withDockerRegistry(credentialsId: 'ecr:eu-west-2:jenkins_aws', url: 'https://380987008477.dkr.ecr.eu-west-2.amazonaws.com') {
        sh "docker push 380987008477.dkr.ecr.eu-west-2.amazonaws.com/spring-boot-mongo"
      }
    }
  }
  
  stage("Deploy To K8s Cluster"){
    steps {
      kubernetesDeploy(
        configs: 'springBootMongo.yml', 
        kubeconfigId: 'KubeConfig',
        secretName: 'eu-west-2-ecr-registry'
       )
     }
    }
  }
}
