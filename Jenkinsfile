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
  }
}
