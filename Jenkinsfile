pipeline {
    agent {
        docker
        { 
            image 'postman/newman:latest'
            args '-u=root --entrypoint='
        }  
    }
    parameters {
        choice(name: 'environment', choices: ['preprod_env', 'prod_env', 'test_env'], description: 'Chosissez une environment')
        booleanParam(name: 'selection', defaultValue: true, description: 'Lancer avec chaque test')
        booleanParam(name: 'tous', defaultValue: true, description: 'Lancer tous les test')
    }
    stages {
        stage('lancer le test') {
            steps {
                script {
                if(params.tous==true ){
                sh 'newman run collection.json'
                sh 'newman run collection1.json -e ./envs/preprod_env.json'
                sh 'newman run collection1.json -e ./envs/test_env.json'
                sh 'newman run collection2.json -e ./envs/prod_env.json'
                }else if (params.selection){
                    sh 'newman run collection.json'
                }
                else{
                    switch(params.environment) {
                        case prod:
                            sh 'newman run collection2.json -e' +${params.environment}+.'json'
                        break
                        default
                        sh 'newman run collection1.json -e' + ${params.environment}+ '.json'
                        sh 'newman run collection1.json -e'+ ${params.environment}+'.json'
                        }
                    }        
                }
            }    
        }
    }
}