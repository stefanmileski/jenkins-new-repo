node {
    def app
    stage('Clone repository') {
        checkout scm
    }
    stage('Build image') {
       app = docker.build("stefanmileski/jenkins-new-repo")
    }
    stage('Push image') {   
        docker.withRegistry('https://registry.hub.docker.com', 'f37ed285-3f44-458c-b238-5b2daf4c2e83') {
            app.push("${env.BRANCH_NAME}-${env.BUILD_NUMBER}")
            app.push("${env.BRANCH_NAME}-latest")
            // signal the orchestrator that there is a new version
        }
    }
}
