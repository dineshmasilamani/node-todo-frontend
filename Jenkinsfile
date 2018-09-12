node {
    
	

    env.AWS_ECR_LOGIN=true
    def newApp
    def registry = 'dineshmasilamani5/transporter_test'
    def registryCredential = 'Smileplease@1'
	
	stage('Git') {
		git 'https://github.com/dineshmasilamani/node-todo-frontend.git'
	}
	stage('Build') {
		sh 'npm install'
		sh 'npm run bowerInstall'
	}
	stage('Test') {
		sh 'npm test'
	}
	stage('Building image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
		    def buildName = registry + ":$BUILD_NUMBER"
			newApp = docker.build buildName
			newApp.push()
        }
	}
	stage('Registring image') {
        docker.withRegistry( 'https://' + registry, registryCredential ) {
    		newApp.push 'latest'
        }
	}
    stage('Removing image') {
        sh "docker rmi $registry:$BUILD_NUMBER"
        sh "docker rmi $registry:latest"
    }
    
}
