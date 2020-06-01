def label = "jenkinsagent-${UUID.randomUUID().toString()}"
podTemplate(containers: [
  containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-8-alpine', ttyEnabled: true, command: 'cat')
  ], volumes: [
  persistentVolumeClaim(mountPath: '/root/.m2/repository', claimName: 'pvc', readOnly: false)
  ]) {

  node(label) {
    stage('Build a Maven project') {
      git 'https://github.com/amenaafreen/simple-java-maven-app.git'
      container('maven') {
          sh 'mvn -B clean package'
      }
    }
  }
}
