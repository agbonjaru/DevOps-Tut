node{
  def app 
  
  stage('clone repository') {
     /* lets make sure we have the repository cloned to out workspace*/
     
  checkout scm
  }

  stage('Build image'){
  /* This builds the actual image; synonymous to docker build
  * on command line */
  
  app = docker.build("agbonjaru/josh-app")
  }
  
 stage('Test image'){
  /*ideally we ould run a test framework against our image
  * For this example, we are using volkswagen type approach */
  
  app.inside {
  sh ' echo "Tests Passed" '
  }
 }
 
 stage('Push image') {
  /* Finally, we l push the image with two tags:
  * First, the incremental build umber from Jenkins
  * Second the latest tag
  * Printing multiple tags is cheap, as all the layers are reused */
  
  docker withRegistry('https://registry.hub.docker.com', 'jstryngs') {
    app.push("$(env.BUILD_NUMBER)")
    app.push("latest")
    
  }
 }
}
