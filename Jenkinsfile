podTemplate(
  name: 'build-pod',
  label: 'build-pod',
  containers: [
      containerTemplate(name: 'docker', image:'trion/jenkins-docker-client'),
      containerTemplate(name: 'helm', image:'linkyard/docker-helm')
  ],
  volumes: [
      hostPathVolume(mountPath: '/var/run/docker.sock',hostPath: '/var/run/docker.sock')
     ]
  ){
    //node = the pod label
    node('build-pod'){
      stage('Build') {
        container('docker') {
              sh 'docker build -t hello-world .'
              sh 'helm package hellojenkins-chart'

        }
      }

      stage('Deploy'){
        container('helm'){
            sh 'helm install hellojenkins-chart-0.6.0.tgz --name helloworld'
        }
      }
    }
  }