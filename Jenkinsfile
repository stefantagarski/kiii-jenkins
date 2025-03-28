node {
    def app
    stage('Clone repository') {
        checkout scm
    }

    if (env.BRANCH_NAME == 'dev') { 
        stage('Build image') {
            app = docker.build("stefantagarski/kiii-jenkins")
        }
        stage('Push image') {   
            docker.withRegistry('https://registry.hub.docker.com', 'dockerhub') {
                app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
                app.push("${env.BRANCH_NAME}-latest")
            }
        }
    } else {
        echo "Skipping Build & Push since this is not the 'dev' branch."
    }
}
