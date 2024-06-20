pipeline {
    agent any
    environment {
        leenewcredentials = credentials('leenewcredentials')
    }
    stages {
        stage('Create Secret & DB') {
            steps {
                sh "sed -e 's,{{SECRET_KEY}},'${leenewcredentials}',g;' secret.yaml | kubectl apply -f -"
            }
        }
        stage('Deploy App') {
            steps {
                sh "kubectl apply -f flask-app.yaml"
                sh "sleep 50"
                sh "kubectl get svc flask-app"
            }
        }
        stage('Deploy NGINX') {
            steps {
                sh "kubectl apply -f nginx.yaml"
                sh "sleep 50"
                sh "kubectl get svc nginx"
            }
        }
    }
}