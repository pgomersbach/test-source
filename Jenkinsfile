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
      stage('get code / compile / stage for docker') {
          container('maven') {
              sh 'git clone -b master https://${USERNAME}:${PASSWORD}@bitbucket.org/mnwgp/mn-wgp.git'
              sh 'cd mn-wgp && ls -l'
              sh 'ls -l'
              sh 'mvn package "-Dtest=*Test, !*ApplicationTest*" "-Dmaven.exec.skip=true"'
          }
      }

//      stage('Maven Build') {
//          container('maven') {
//              dir('hello-world-war/') {
//                  sh 'hostname'
//                  sh 'hostname -i'
//                  sh 'mvn clean install'
//              }
//          }
//      }
    }
  }
}
