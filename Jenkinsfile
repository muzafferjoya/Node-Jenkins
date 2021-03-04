node {
    
    stage('Git clone'){
        git 'https://github.com/muzafferjoya/Node-Jenkins.git'
    }

    stage('Install Dependencies'){
	   sh 'npm install'
}

    stage('Test and Build'){
        parallel {
            stage('Run Tests'){
                steps {
                    sh 'npm run test'
                }
            }
            stage('Create Build Artifacts'){
                steps {
                    sh 'npm run build'
                }
            }
        }
    }

    
    stage('AWS Credentials Check') {

        dir('/var/lib/jenkins/workspace/build-node'){

        pwd(); 

        withAWS(region:'us-east-1',credentials:'aws-id') {

        def identity=awsIdentity();
		
		s3Upload(bucket: "muzaffar-node", workingDir: '.', includePathPattern:'**/*', excludePathPattern:'.git/*', excludePathPattern: 'node_modules/*');
                 
        }

        };

	}
}
