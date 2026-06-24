pipeline {
    agent {
        docker
        { 
            image 'postman/newman:latest'
            args '-u=root --entrypoint='
        }  
    }

    stages {
        stage('lancer le test') {
            steps {
                sh 'newman run collection.json'
            }
        }
    }
}
