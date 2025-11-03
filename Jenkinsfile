pipeline {
    agent any

    environment {
        KUBECONFIG = '/root/.kube/config'
    }

    stages {
        stage('Checkout') {
            steps {
                git branch: 'main', url: 'https://github.com/aiden-panvalkar/k8s-gitops-demo.git'
            }
        }

        stage('Deploy to Kubernetes') {
            steps {
                script {
                    if (env.BRANCH_NAME == 'dev') {
                        echo "Deploying polling-app to DEV namespace..."
                        sh 'kubectl apply -f polling-app/dev/ --namespace=dev'
                    } else if (env.BRANCH_NAME == 'prod') {
                        echo "Deploying polling-app to PROD namespace..."
                        sh 'kubectl apply -f polling-app/prod/ --namespace=prod'
                    } else {
                        echo "This branch is not configured for deployment."
                    }
                }
            }
        }
    }
}
