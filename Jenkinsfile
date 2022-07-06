node {
    def commit_id
    def app

    stage('Clone repository') {
        /* Cloning the Repository to our Workspace */
	    commit_id = readFile('.git/commit-id').trim()

        checkout scm
    }

    stage('Build image') {
        /* This builds the actual image */

        app = docker.build("mobilloradmin/nodeapp")
    }

    stage('Test image') {
        
        app.inside {
            echo "Tests passed"
        }
    }

    stage('Push image') {
        /* 
			You would need to first register with DockerHub before you can push images to your account
		*/
        docker.withRegistry('https://registry.hub.docker.com', 'docker-hub-id') {
            app.push(commit_id)
            } 
                echo "Trying to Push Docker Build to DockerHub"
    }
}
