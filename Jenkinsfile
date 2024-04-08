pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Étape pour récupérer le code depuis Git
                git branch: 'develop', url: 'https://github.com/hianeme/jenkins_test.git'
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
                    def timestamp = new Date().format('yyyy-MM-dd_HH-mm-ss') // Timestamp actuel pour le nom de sauvegarde
                    def newDir = "current_${timestamp}"
                    // Obtention des fichiers à envoyer
                    // def filesToSend = sh(script: "ls", returnStdout: true).trim().split("\n")
                    def fileList = sh(script: "ls", returnStdout: true).trim().split()

                    // Utilisation de lftp pour transférer les fichiers et dossiers de manière récursive
                    
                    
                    // Utilisation de la commande curl pour renommer le répertoire current
                    // sh "curl -Q 'RNFR current' -Q 'RNTO backup_${timestamp}' ftp://${user}:${password}@${server}${remoteDir}/"

                    // Utilisation de la commande curl pour envoyer les fichiers
                    fileList.each { file ->
                        sh "curl --ftp-create-dirs -T ${file} ftp://${user}:${password}@${server}${remoteDir}/current/"
                        // sh "curl --ftp-create-dirs -T ${fileList.join(' ')} ftp://${user}:${password}@${server}${remoteDir}/${newDir}/"
                    }
                }
            }
        }
    }
}
