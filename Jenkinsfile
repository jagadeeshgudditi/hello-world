pipeline {
    agent any

    stages {
        stage('Get Latest Code') {
            steps {
                echo 'Get Latest Code'
				// Get some code from a GitHub repository
                git 'https://github.com/jagadeeshgudditi/hello-world.git'
            }
        }
		stage('Clean the Workspace') {
            steps {
                echo 'Clean the Workspace'
				// Run Maven on a Unix agent.
                sh "mvn clean"
            }
        }
		stage('Compile') {
            steps {
                echo 'Compile'
				// Run Maven on a Unix agent.
                sh "mvn clean compile"
            }
        }
		stage('Test') {
            steps {
                echo 'Test'
				// Run Maven on a Unix agent.
                sh "mvn clean compile test"
				
            }
        }
		stage('Package the Solution') {
            steps {
                echo 'Package the Solution'
				// Run Maven on a Unix agent.
                sh "mvn clean compile package"
            }
        }
		stage('Deploy to UAT') {
            steps {
                input 'Do you want to continue deploymen to UAT?'
				echo 'Deploy to UAT'
				
            }
        }
		
    }
}
