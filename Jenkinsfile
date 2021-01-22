node {
    def app

    stage('Clone repository') {
        checkout scm
    }

    stage('Build image') {
       app = docker.build("sujee/jenkins-docker1")
    }

    // stage('Test image') {
    //     app.inside {
    //         sh 'echo "Tests passed"'
    //     }
    // }

    stage('Push image') {
        docker.withRegistry('https://registry.hub.docker.com', 'dockerhub-sujee') {
            app.push("${env.BUILD_NUMBER}")
            app.push("latest")
        }
    }
}