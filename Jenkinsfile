import groovy.json.JsonSlurperClassic

def getDashboard(url){
	withCredentials([string(credentialsId: 'OctopusApiKey', variable: 'OctopusApiKey')]){
		def resp = httpRequest(
			customHeaders: [[maskValue: false, name: 'X-Octopus-ApiKey', value: OctopusApiKey]],
			url: url
		)

		assert resp.status == 200 : "dashboard not found! Check Octopus server"
		def content = new JsonSlurperClassic().parseText(resp.content)
		return content
	}
}

def filterId(content, filter) {
    for (int k=0; k<content.size(); k++){
        def item = content[k]
        if (item["Name"] == filter) {
            id = item["Id"]
        }
    }
    return id
}

@NonCPS
def getTaskId(list, projId, envId, releaseVersion) {
    def res
    list.each { item ->
	if (item['ProjectId'] == projId  && item['EnvironmentId'] == envId && item['ReleaseVersion'] == releaseVersion){
		res = item['TaskId']
		print(res)
	    }
    }
	return res
}

node('windows') {
    ansiColor('xterm') {
        cleanWs()
        def workspace = pwd()
        def branch = env.BRANCH_NAME
        def scmVars = checkout scm
        def branchName = scmVars.GIT_BRANCH
        def cid = env.CHANGE_ID
        def LICENSE_URL = "https://nmaltsevastorage.blob.core.windows.net/sandbox/license.xml"
        if(env.CHANGE_ID && branch != 'develop') {
            stage('Build'){
                powershell """
                    Write-Output "branch: ${branch}"
                    Write-Output "scmVars: ${scmVars}"
                    Write-Output "cid: ${cid}" """
            }
            stage('Preparation'){
             powershell """
                    Write-Output "Downloading license.xml file"
                    Write-Output "${ENV:LICENSE_URL}"
                    Invoke-WebRequest -Uri ${ENV:LICENSE_URL} -OutFile "${workspace}\\license.xml"
                """
            }
        } else {
            echo "${scmVars}"
            echo "cid: ${cid}"
        }
    }
}
