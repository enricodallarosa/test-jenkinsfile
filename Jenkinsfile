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
                      buildDirName = "$BUILD_ID"
                      workingDir = "$baseDir/$buildDirName"
                      withCredentials([sshUserPrivateKey(credentialsId: 'agent-windows-105', keyFileVariable: 'identity', passphraseVariable: '', usernameVariable: 'userName')]) {
                          remote.user = userName
                          remote.identityFile = identity
                          stage('sshWindows') {
                            sshCommand remote: remote, command: "cd $baseDir && mkdir $buildDirName"
                          }
                      }
                }
            }
        }
    }
}
