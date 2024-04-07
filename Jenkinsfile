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
                // Utilisation du plugin Publish Over FTP pour pousser les fichiers sur le serveur FTP
                script {
                    def server = 'nom_de_votre_configuration_ftp' // Nom de la configuration FTP définie dans Jenkins
                    def remoteDirectory = '/remote/directory' // Répertoire distant sur le serveur FTP
                    def credentialsId = 'identifiants' // ID des identifiants de connexion FTP définis dans Jenkins

                    // Obtention des fichiers à envoyer
                    def filesToSend = findFiles(glob: '**/*')

                    // Utilisation de la fonction 'publishOverFTP' pour envoyer les fichiers
                    publishOverFTP (
                        failOnError: true,
                        serverSelection: server,
                        transfers: [
                            [
                                sourceFiles: filesToSend,
                                remoteDirectory: remoteDirectory,
                                flatten: false
                            ]
                        ],
                        transferSetSource: 'PROJECT'
                    )
                }
            }
        }
    }
}
