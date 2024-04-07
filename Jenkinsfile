pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Étape pour récupérer le code depuis Git
                git branch: 'develop, url: 'https://github.com/hianeme/jenkins_test.git'
            }
        }
        
        stage('Push to FTP') {
            steps {
                // Utilisation de curl pour envoyer les fichiers sur le serveur FTP
                script {
                    def server = 'ftpupload.net' // Adresse IP ou nom de domaine du serveur FTP
                    def user = 'b11_36320483' // Nom d'utilisateur FTP
                    def password = 'lorem1357\\$\\$' // Mot de passe FTP
                    def remoteDir = '/htdocs' // Répertoire distant sur le serveur FTP

                    // Obtention des fichiers à envoyer
                    def filesToSend = sh(script: "ls", returnStdout: true).trim().split("\n")

                    // Utilisation de la commande curl pour envoyer les fichiers
                    filesToSend.each { file ->
                        sh "curl -T ${file} ftp://${user}:${password}@${server}${remoteDir}/"
                    }
                }
            }
        }
    }
}
