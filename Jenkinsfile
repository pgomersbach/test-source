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
    container('maven') {
      stage('git checkout') {
          sh 'git clone -b master https://github.com/pgomersbach/test-source.git .'
//        sh 'git clone -b master https://${GIT_USERNAME}:${GIT_PASSWORD}@bitbucket.org/mnwgp/mn-wgp.git'
//        sh 'echo $SLACK_URL $DOCKER_REGISTRY'
          sh 'pwd'
          sh 'ls -la'
      }
      stage('maven package') {    
          sh 'mvn package'
//          sh 'mvn surefire-report:report-only'
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
