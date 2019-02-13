pipeline {
    agent any
    stages {
        stage('Build Back'){
            steps {
                dir('/var/lib/jenkins/workspace') {
                    sh "tar -zcvf movie-analyst-api.tar.gz Backend_master"
                    sh "mkdir -p Artifacts_repo" 
                    sh "mv movie-analyst-api.tar.gz Artifacts_repo"
            }     
            }
        }
        stage('Deploy Back Server'){
            steps {
               dir('/var/lib/jenkins/workspace/Artifacts_repo') {               
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ubuntu@11.0.3.105', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: ' tar xvzf movie-analyst-api.tar.gz && rsync -rpa Backend_master/ movie-analyst-api && pm2 stop && pm2 start ', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'tar xvzf movie-analyst-api.tar.gz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])        
           }
        }  
        stage("Restart Service"){
            steps {   
               sh ' ssh ubuntu@11.0.3.105 echo Hello'   
           }
        }  
    }
}

    
    
