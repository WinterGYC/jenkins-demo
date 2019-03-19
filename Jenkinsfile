pipeline{
      agent{
        node{
          label 'slave-pipeline'
        }
      }

      stages{
        stage('Set up PV/PVC') {
          steps {
            container('kubectl') {
              step([$class: 'KubernetesDeploy', authMethod: 'certs', apiServerUrl: 'https://kubernetes.default.svc.cluster.local:443', credentialsId:'k8sCertAuth', config: 'AlibabaCloud/persistent-volume/pvc-test.yaml', variableState: 'VarState'])
            }
          }
        }

        stage('Set up DBs') {
          parallel {
            stage('Set up MySQL') {
              steps {
                container('kubectl') {
                  step([$class: 'KubernetesDeploy', authMethod: 'certs', apiServerUrl: 'https://kubernetes.default.svc.cluster.local:443', credentialsId:'k8sCertAuth', config: 'AlibabaCloud/mysql/mysql-deployment-test.yaml', variableState: 'VarState'])
                }
              }
            }

            stage('Set up MongoDB') {
              steps {
                container('kubectl') {
                  step([$class: 'KubernetesDeploy', authMethod: 'certs', apiServerUrl: 'https://kubernetes.default.svc.cluster.local:443', credentialsId:'k8sCertAuth', config: 'AlibabaCloud/mongo/mongo-deployment-test.yaml', variableState: 'VarState'])
                }
              }
            }
            stage('Set up Redis') {
              steps {
                container('kubectl') {
                  step([$class: 'KubernetesDeploy', authMethod: 'certs', apiServerUrl: 'https://kubernetes.default.svc.cluster.local:443', credentialsId:'k8sCertAuth', config: 'AlibabaCloud/redis/redis-deployment-test.yaml', variableState: 'VarState'])
                }
              }
            }
          }
        }

        stage('Load Mongo Data') {
          steps {
              container('kubectl') {
                  step([$class: 'KubernetesDeploy', authMethod: 'certs', apiServerUrl: 'https://kubernetes.default.svc.cluster.local:443', credentialsId:'k8sCertAuth', config: 'AlibabaCloud/mongo/mongo-applier.yaml', variableState: 'VarState'])
              }
          }
        }

        stage('Set up bigbang') {
          steps {
              container('kubectl') {
                  step([$class: 'KubernetesDeploy', authMethod: 'certs', apiServerUrl: 'https://kubernetes.default.svc.cluster.local:443', credentialsId:'k8sCertAuth', config: 'AlibabaCloud/bigbang/bigbang-deployment-test.yaml', variableState: 'VarState'])
              }
          }
        }
      }
    }
