pipeline {
    agent any
      parameters {
        choice(
            name: 'Environment',
            choices: ['main', 'dev', 'qa'],
            description: 'Please Select env'
        )
    }
     tools {
        // Install the Maven version configured as "M3" and add it to the path.
        maven "maven"
    }
    environment {
        GIT_URL = "https://github.com/choudharyjayant/sample-java-project-jenkins-codedeploy.git"
        ARTIFACT_BUILD = "jb-hello-world-maven-0.2.0.jar"
        Zip_Name = "${BUILD_NUMBER}.zip"
      
      
    }
    stages {
       
        stage('verifying tools') {
            steps {
                sh ''' #! /bin/bash
                java -version
		        mvn --version
                '''
            }
        }
        stage('Build') {
            steps {
                sh ''' #! /bin/bash
                #Ignoring test cases 
                mvn install -DskipTests
             
                
                '''
            }
        }
        stage ('Test') {
            steps {
                sh ''' #! /bin/bash
                mvn test
                '''
            }
        }
		stage ('Artifact') {
               steps {
               withCredentials([[ $class: 'AmazonWebServicesCredentialsBinding', credentialsId: 'aws-cred-2']]) {
      
                sh """ #!/bin/bash               
                sudo zip -r ${env.Zip_Name} appspec.yml Dependency_Scripts target/${env.ARTIFACT_BUILD}
                #To push zip folder to s3 
                aws s3 cp ${env.Zip_Name}  s3://${env.bucket_name}/
                """
            }
        }
		}
        
        }
       
    }
    post {
        always {
            echo 'Stage is success'
        }
    }
    }
