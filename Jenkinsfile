pipeline{
    
  agent { label "kubepod" }

  stages {

  stage("Git Clone"){
    step {
      git credentialsId: 'Jenkins-Git', url: 'https://github.com/radek5/spring-boot-mongo-docker.git'
    }
  }
   
  stage("Maven Clean Build"){
    step {
      def mavenHome = tool name: "Maven-3.6.3", type: "maven"
      def mavenCMD = "${mavenHome}/bin/mvn"
      sh "${mavenCMD} clean package"
    } 
  }
    
  stage("Build Docker Image"){
    step {
      sh "docker build -t 380987008477.dkr.ecr.eu-west-2.amazonaws.com/spring-boot-mongo ."
    }
  }
    
  stage("Push Docker Image"){
    step {
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
