def registry = 'https://trial3tt8b4.jfrog.io/' 
def imageName = 'sagar1993.jfrog.io/sagar-docker-local/ttrend'
   def version   = '2.0.2'
pipeline{
    agent {
        node { 
           label "maven-agent"
        }
    }
    environment {
        PATH = "/opt/apache-maven-3.9.9/bin:$PATH"
    }
    stages {
        stage ('build') {
            steps {
                sh 'mvn clean deploy'
           
             }
        }
  //  }
//}    
       /*stage ('SonarQube analysis') {
        environment {
          scannerHome = tool 'SonarQube-Scanner' 
        }
            steps {
            withSonarQubeEnv('SonarQube-Server') 
              {
             sh '${scannerHome}/bin/sonar-scanner'
    }    
            }
        }
    }

}*/
    
     
         stage("Jar Publish") {
        steps {
            script {
                    echo '<--------------- Jar Publish Started --------------->'
                     def server = Artifactory.newServer url:registry+"/artifactory" ,  credentialsId:"sagar"
                     def properties = "buildid=${env.BUILD_ID},commitid=${GIT_COMMIT}";
                     def uploadSpec = """{
                          "files": [
                            {
                              "pattern": "jarstaging/(*)",
                              "target": "mavne-n-libs-release-local/{1}",
                              "flat": "false",
                              "props" : "${properties}",
                              "exclusions": [ "*.sha1", "*.md5"]
                            }
                         ]
                     }"""
                     def buildInfo = server.upload(uploadSpec)
                     buildInfo.env.collect()
                     server.publishBuildInfo(buildInfo)
                     echo '<--------------- Jar Publish Ended --------------->'  
            
            }
        }   
    }   
  //  }
//}


   /* stage(" Docker Build ") {
      steps {
        script {
           echo '<--------------- Docker Build Started --------------->'
           app = docker.build(imageName+":"+version)
           echo '<--------------- Docker Build Ends --------------->'
        }
      }
    }

            stage (" Docker Publish "){
        steps {
            script {
               echo '<--------------- Docker Publish Started --------------->'  
                docker.withRegistry(registry, 'nani'){
                    app.push()
                }    
               echo '<--------------- Docker Publish Ended --------------->'  
            }
        }
    }
          //   stage("deployment"){
            //  steps {
              //  script{
                //  //sh './deploy.sh'
                  //sh 'helm install ttrend-1 ttrend-1-0.1.0.tgz'
                //}
              //}
    //}
    } 
}*/
    }
}
