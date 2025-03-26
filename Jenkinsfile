@Library("Shared") _
pipeline{
    agent {label "vinod"}
    stages{
        stage("Clone"){
            steps{
            script{
          clone("https://github.com/AdityaSoni7728/django-notes-app.git","main")
            }
        }}
        stage("Build"){
            steps{
          script{
              docker_build("notes-app","latest","AdityaSoni7728")
          }
           
            
        }}
        stage("Pushing to Dockerhub"){
            steps{
            echo "This is pushing the code"
             withCredentials([usernamePassword(
                    credentialsId:"dockerHubCred",
                    usernameVariable:"dockerHubUser", 
                    passwordVariable:"dockerHubPass")]){
            sh "docker login -u  ${env.dockerHubUser} -p ${env.dockerHubPass}"
            sh "docker image tag notes-app:latest  ${env.dockerHubUser}/notes-app:latest"
            sh "docker push  ${env.dockerHubUser}/notes-app:latest"
        }}}
        stage("Deploy"){
            steps{
           echo "This is deploying the code"
        sh "docker compose down && docker compose up -d"
        echo "Deployment successful"
        }}
    }
} 
