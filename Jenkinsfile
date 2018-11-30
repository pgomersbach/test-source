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
    withEnv(["SLACK_URL=https://hooks.slack.com/services/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s","DOCKER_REGISTRY=https://registry.hub.docker.com/v2"]) {
      withCredentials([[$class: 'UsernamePasswordMultiBinding', credentialsId: 'GIT_CREDENTIALS',usernameVariable: 'GIT_USERNAME', passwordVariable: 'GIT_PASSWORD']]) {
        stage('get code / compile / stage for docker') {
          container('maven') {
            sh 'git clone -b master https://${GIT_USERNAME}:${GIT_PASSWORD}@bitbucket.org/mnwgp/mn-wgp.git'
            sh 'echo $SLACK_URL $"DOCKER_REGISTRY'
            dir ('mn-wgp') {
              sh 'mvn package "-Dtest=*Test, !*ApplicationTest*" "-Dmaven.exec.skip=true"'
              sh 'mvn surefire-report:report-only'
            }
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
}
