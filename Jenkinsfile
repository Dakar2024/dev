pipeline { 
    agent any

    environnement {
        VENV_DIR="venv"
    }

    stages { 
        stage('Checkout') { 
            steps { 
                git branch: 'main', url: 'https://github.com/Dakar2024/dev.git' 
            } 
        } 
        stage('Install Dependencies') { 
            steps { 
                bat 'python -m venv venv' 
            } 
        }
 
        stage('Run Script') { 
            steps { 
                bat '.\\venvbin\\python TP4.py' 
            } 
        } 
    }
 
    post { 
        success { 
            emailext subject: "Build SUCCESS: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: "Le build de ${env.JOB_NAME} a réussi.\nConsultez les logs ici: ${env.BUILD_URL}",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                    to: 'dakaroctobre2024@gmail.com'
        } 
        failure { 
            emailext subject: "Build FAILURE: ${env.JOB_NAME} #${env.BUILD_NUMBER}",
                    body: "Le build de ${env.JOB_NAME} a échoué.\nConsultez les logs ici: ${env.BUILD_URL}",
                    recipientProviders: [[$class: 'DevelopersRecipientProvider']],
                    to: 'dakaroctobre2024@gmail.com'
        } 
    }

    }
