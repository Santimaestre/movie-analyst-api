pipeline {
    agent any
    stages {
       stage('Clone Back') {
            steps {
                sh "rm -rf movie-analyst-api"
                sh "git clone https://github.com/ScastellanosM/movie-analyst-api.git"
            }
        }
        stage('Build Front'){
            steps {
                sh "zip -r movie-analyst-api.zip /var/lib/jenkins/workspace/Back_master"      
            }
        }
        stage('Deploy Back Server'){
            steps {
               sshPublisher(publishers: [sshPublisherDesc(configName: 'ubuntu@11.0.1.17', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'echo "Hello Front A"', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'movie-analyst-ui.zip')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])
           }
        }  
    }
}
