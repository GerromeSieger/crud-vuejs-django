pipeline {
    agent any
    environment {
        DHUB = credentials('dockerhub')
    }
    stages {

        stage('Docker deploy') {
                agent any
            steps {
                sh 'ssh -o StrictHostKeyChecking=no victor@192.168.56.107 && cd crud-vuejs-django'
                sh 'docker-compose pull && docker-compose up'
            }  
        }        
        stage('Docker build') {
                agent any
            steps {
                sh 'cd subscription-api && docker build -t gerrome/crud-vuejs-django_backend:1.2 .'
                sh 'cd subscription-app && docker build -t gerrome/crud-vuejs-django_nginx:1.2 .'  
            }                                        
        }  
            
        stage('Docker push') {
                agent any
            steps {
                sh 'docker login -u ${DHUB_USR} -p ${DHUB_PSW} && docker push gerrome/crud-vuejs-django_backend:1.2' 
                sh 'docker login -u ${DHUB_USR} -p ${DHUB_PSW} && docker push gerrome/crud-vuejs-django_nginx:1.2'                            
            }
        }

    }
    post { 
        always { 
            echo 'I will always say Hello again!'
        }
    }
}
