pipeline{
      // 定义本次构建使用哪个标签的构建环境，本示例中为 “slave-pipeline”
      agent{
        node{
          label 'slave-pipeline'
        }
      }

      // "stages"定义项目构建的多个模块，可以添加多个 “stage”， 可以多个 “stage” 串行或者并行执行
      stages{
        // 定义第一个stage， 完成克隆源码的任务
        stage('Git'){
          steps{
            git branch: 'master', credentialsId: '', url: 'https://github.com/WinterGYC/jenkins-demo.git'
          }
        }

        stage('Set up MySQL') {
          steps {
            container('kubectl') {
              step([$class: 'KubernetesDeploy', authMethod: 'certs', apiServerUrl: 'https://kubernetes.default.svc.cluster.local:443', credentialsId:'k8sCertAuth', config: '/home/jenkins/workspace/demo-pipeline/mysql/mysql-deployment-test.yaml'])
            }
          }
        }
      }
    }
