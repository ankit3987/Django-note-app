pipeline {
    agent any
    
    stages{
        stage("Code"){
            steps {
                echo "cloing the code"
                git url:"https://github.com/LakshyaGulenia/Django-notes-app.git", branch: "main"
            }
            
        }
        stage("build"){
            steps {
                echo "building the code"
                sh "docker build -t my-notes-app ."
            }
            
        }
        // stage("push to Docker hub"){
        //     steps {
        //         echo "pushing the image to docker hub"
        //         withCredential([usernamepassword(credentialsId:"dockerHub",passwordVariable:"dockerHubPass",usernameVariable:"dockerHubUser")]){
        //         sh "docker tag my-notes-app ${env.dockerHubUser}/my-notes "
        //         sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
        //         sh "docker push ${env.dockerHubUser}/my-notes"
                    
        //         }
        //     }
            
        // }
        stage("Push to Docker hub"){
            steps{
                echo "pushing the image to docker hub"
                withCredentials(
			[usernamePassword(
				credentialsId:"dockerHub",
				passwordVariable:"dockerHubPass",
				usernameVariable:"dockerHubUser"
				)
			]		
		){
                sh "docker tag my-note-app ${env.dockerHubUser}/my-note-app:latest"
                sh "docker login -u ${env.dockerHubUser} -p ${env.dockerHubPass}"
                sh "docker push ${env.dockerHubUser}/my-note-app:latest"
                }
            }
        }
        stage("Deploy"){
            steps {
                echo "deploing the container"
                sh "docker run -d -p 8000:8000 ${env.dockerHubUser}/my-notes"
            }
            
        }
    }
}
