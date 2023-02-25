def execOnWindows = true;
pipeline {
    agent {label "linux"}
    stages {
        stage('exec on windows') {
            when {
                expression {execOnWindows == true}
            }
            steps {
                script {
                      def remote = [:]
                      //remote.name = 'windows-10.39.4.105-ssh'
                      remote.name = '10.39.4.105'
                      remote.host = '10.39.4.105'
                      remote.allowAnyHosts = true
                      baseDir = "/Users/daen/jenkins_agent_test_data"
                       buildDirName = "$BRANCH_NAME-$BUILD_ID"
                      workingDir = "$baseDir/$buildDirName"
                      withCredentials([sshUserPrivateKey(credentialsId: 'agent-windows-105', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                          remote.user = userName
                          remote.identityFile = identity
                          stage('sshWindows') {
                            sshCommand remote: remote, command: "cd $baseDir && mkdir $buildDirName"
                            sshCommand remote: remote, command: "cd $baseDir && copy script.bat $buildDirName"
                            sshCommand remote: remote, command: "cd $baseDir && copy windows_text.txt $buildDirName"
                            
                            sshPut remote: remote, from: "../linux_text.txt", into: "$workingDir/linux_text.txt"
                            sshCommand remote: remote, command: "cd $workingDir && script.bat"
                            sshGet remote: remote, from: "$workingDir/out.txt", into: "out.txt", override: true
                            sshRemove remote: remote, path: "$workingDir/out.txt"
                            sshCommand remote: remote, command: "cd $baseDir && rmdir $buildDirName /S /Q"
                          }
                      }
                }
            }
        }
    }
}
