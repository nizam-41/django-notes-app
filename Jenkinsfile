@Library("Shared") _
pipeline{
    
    agent{ label "vinod" }
    
    stages {
        
        stage("hello"){
            steps{
                script{hello()
                    
                }
            }
        }
        stage("Code"){
            steps{
                script{
                clone("https://github.com/nizam-41/django-notes-app", "dev")
                }
            }
        }
        stage("Build"){
             steps{
                script{
                 docker_build("notes-app","latest","nizam-41")
                }
             }
        }
        stage("Test"){
             steps{
                 echo "This is testing the code"
             }
        }
        stage("Push to DockerHub") {
    steps {
        docker_push(
            imageName: "notes-app",
            imageTag: "latest",
            credentials: "DockerHubCred"
        )
    }
}
        stage("Deploy"){
    steps{
        echo "This is deploying the code"
        sh "docker compose down && docker compose up -d"
        }
       }
    }
}
