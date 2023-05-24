pipeline {
  agent any
  
  stages {
    stage('Checkout') {
      steps {
        // Checkout the source code from your Git repository
        git 'https://github.com/pratik8595/color-test-app-node.js.git'
      }
    }
    
    stage('Build') {
      steps {
        // Build the Node.js application
        sh 'npm install'
        sh 'npm test'
      }
    }
    
    stage('Build Docker Image') {
      steps {
        // Build the Docker image for your application
        sh 'docker build -t nodejs .'
      }
    }
    
    stage('Push Docker Image') {
      steps {
        // Push the Docker image to your Docker registry
        sh 'docker push 890624094034.dkr.ecr.ap-northeast-1.amazonaws.com/nodejs'
      }
    }
    
    stage('Deploy to ECS') {
      steps {
        // Deploy the application to ECS
        sh '''
          export AWS_REGION=ap-northeast-1
          export ECS_CLUSTER=nodejs_cluster
          export ECS_SERVICE=s1
          
          # Update ECS service with new task definition
          ecs-cli compose --project-name 'color-test-app-node.js' service up --force-deployment --cluster-config nodejs_taskdef
        '''
      }
    }
  }
}
