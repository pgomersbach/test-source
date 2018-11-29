podTemplate(label: 'mypod', containers: [
    containerTemplate(name: 'git', image: 'alpine/git', ttyEnabled: true, command: 'cat'),
    containerTemplate(name: 'maven', image: 'maven:3.5-jdk-8', command: 'cat', ttyEnabled: true),
    containerTemplate(name: 'docker', image: 'docker', command: 'cat', ttyEnabled: true)
  ],
  volumes: [
    hostPathVolume(mountPath: '/var/run/docker.sock', hostPath: '/var/run/docker.sock'),
  ]
  ) {
    node('mypod') {
      withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'git_credentials',usernameVariable: 'USERNAME', passwordVariable: 'PASSWORD']]) {
      stage('Clone repository') {
          container('git') {
              sh 'echo uname=$USERNAME pwd=$PASSWORD'
              sh 'whoami'
              sh 'hostname -i'
              sh 'git clone -b master https://${USERNAME}:${PASSWORD}@bitbucket.org/mnwgp/mn-wgp.git'
#              sh 'git clone -b master https://github.com/lvthillo/hello-world-war.git'
          }
      }

#      stage('Maven Build') {
#          container('maven') {
#              dir('hello-world-war/') {
#                  sh 'hostname'
#                  sh 'hostname -i'
#                  sh 'mvn clean install'
#              }
#          }
#      }
    }
  }
}
