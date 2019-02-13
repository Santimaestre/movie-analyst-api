pipeline {
    agent any
    stages {
        stage('Build Back'){
            steps {
                dir('/var/lib/jenkins/workspace') {
                    sh "tar -zcvf movieanalyst-api.tar.gz Backend_master"
                    sh "mkdir -p Artifacts_repo" 
                    sh "mv movieanalyst-api.tar.gz Artifacts_repo"
            }     
            }
        }
        stage('Deploy Back Server'){
            steps {
               dir('/var/lib/jenkins/workspace/Artifacts_repo') {               
                sshPublisher(publishers: [sshPublisherDesc(configName: 'ubuntu@11.0.3.105', transfers: [sshTransfer(cleanRemote: false, excludes: '', execCommand: 'tar xvzf movieanalyst-api.tar.gz |  rsync -rpa Backend_master/ movieanalyst-api', execTimeout: 120000, flatten: false, makeEmptyDirs: false, noDefaultExcludes: false, patternSeparator: '[, ]+', remoteDirectory: '', remoteDirectorySDF: false, removePrefix: '', sourceFiles: 'tar xvzf movieanalyst-api.tar.gz')], usePromotionTimestamp: false, useWorkspaceInPromotion: false, verbose: false)])        
           }
        }  
    }
}
}
