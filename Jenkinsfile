pipeline {

agent any
    
stages{
        
    stage('Git clone'){
        steps{
            git 'https://github.com/muzafferjoya/Node-Jenkins.git'
        }
    }

    stage('Install Packages') {
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
      }
    }

    
    stage('Deploy To S3 Bucket') {

        dir('/var/lib/jenkins/workspace/node-jenkins'){

        pwd(); 

        withAWS(region:'us-east-1',credentials:'aws-id') {

        def identity=awsIdentity();
        
    s3Upload(bucket:"muzaffar-khan", workingDir:'dist', includePathPattern:'**/*', excludePathPattern:'.git/*, **/node_modules/**');
                 
        }

        };

    }
    }
}
