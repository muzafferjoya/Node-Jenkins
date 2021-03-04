node {
    
    stage('Git clone'){
        git 'https://github.com/muzafferjoya/Node-Jenkins.git'
    }

    stage('Install Dependencies'){
	   sh 'npm install'
}

	stage('Test'){
		sh 'npm run test'
	}

	stage('Building'){
		sh 'npm run build'
	}

    
    stage('Deploy To S3 Bucket') {

        dir('/var/lib/jenkins/workspace/build-node'){

        pwd(); 

        withAWS(region:'us-east-1',credentials:'aws-id') {

        def identity=awsIdentity();
		
	s3Upload(bucket:"muzaffar-khan", workingDir:'dist', includePathPattern:'**/*', excludePathPattern:'.git/*, node_modules/*');
                 
        }

        };

	}
}
