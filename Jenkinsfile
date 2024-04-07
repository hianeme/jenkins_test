pipeline {
    agent any

    stages {
        stage('Checkout') {
            steps {
                // Étape pour récupérer le code depuis Git
                git 'https://github.com/hianeme/jenkins_test.git'
            }
        }
        
        stage('Push to FTP') {
            steps {
                script {
                    // Paramètres FTP
                    def ftpServer = 'ftp.example.com'
                    def ftpUser = 'username'
                    def ftpPassword = 'password'
                    def remoteDir = '/remote/directory'

                    // Chemin local vers le code
                    def localDir = "${env.WORKSPACE}"

                    // Connexion FTP
                    def ftp = new FtpClient()
                    ftp.connect(ftpServer)
                    ftp.login(ftpUser, ftpPassword)
                    
                    // Changement du répertoire distant
                    ftp.changeWorkingDirectory(remoteDir)

                    // Liste des fichiers à transférer
                    def fileList = sh(script: "ls ${localDir}", returnStdout: true).trim().split('\n')

                    // Transfert de chaque fichier vers le serveur FTP
                    fileList.each { file ->
                        ftp.putFileStream(file)
                    }

                    // Déconnexion FTP
                    ftp.logout()
                    ftp.disconnect()
                }
            }
        }
    }
}
