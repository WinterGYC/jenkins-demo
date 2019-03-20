pipeline{
      agent{
        node{
          label 'slave-pipeline'
        }
      }

      stages{
        stage('Git'){
          steps{
            git branch: 'master', credentialsId: '', url: 'https://github.com/WinterGYC/jenkins-demo.git'
            dir("bigbang") {
              git branch: 'dev', credentialsId: '', url: 'https://gitlab.rsvptech.ca/dialog/bigbang.git'
            }
            // dir("agents") {
            //   git branch: 'development', credentialsId: '', url: 'https://git.rsvptech.cn/dlz/Agents.git'
            // }
          }
        }
      }
    }
