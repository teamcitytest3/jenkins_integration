
node('windows') {
    ansiColor('xterm') {
        cleanWs()
        def workspace = pwd()
        stage('Build'){
            powershell '''
                Write-Output "Hello!"
                Get-ChildItem -Directory ${workspace} '''
        }
        stage('Preparation'){
            powershell """
                Write-Output "Downloading license.xml file"
                Write-Output "${ENV:LICENSE_URL}"
                Invoke-WebRequest -Uri ${ENV:LICENSE_URL} -OutFile "${workspace}\\license.xml"
            """
        }
    }
}