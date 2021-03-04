pipeline {
        agent any

        tools {nodejs "node-15.11"}

        stages {
              stage('Clone git repository') {
                 steps {
                    git 'https://github.com/muzafferjoya/Node-Jenkins.git'
 }
}
              stage('Install Dependencies') {
                 steps {
                   sh 'npm install'
 }
}
              stage('Test and Build') {
                parallel {
                   stage('Run Tests') {
                      steps {
                        sh 'npm run test'
  }
}

              stage('Create Build Artifacts') {
                steps {
                  sh 'npm run build'
      }
    }
              stage('Deploy Artifacts to S3 Bucket'){
                pwd();
                withAWS(region: 'us-east-1', credentials: 'aws-id'){
                  def identity=awsIdentity();
                  s3Upload(bucket: "muzaffar-node", workingDir: './dist', includePathPattern: '**/*', excludePathPattern: '.git/*', excludePathPattern: 'node_modules/*');
                }

              };
  }
}
}
}
