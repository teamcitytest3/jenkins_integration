
node('windows') {
    ansiColor('xterm') {
        cleanWs()
        def workspace = pwd()
        stage('build'){
            powershell '''
                Write-Output "Hello!" '''
        }
    }
}