def label = "jenkinsagent-${UUID.randomUUID().toString()}"


podTemplate(label: label,
        containers: [
                containerTemplate(name: 'jnlp', image: 'jenkins/jnlp-slave:3.27-1', envVars: [ envVar(key: 'GIT_SSL_NO_VERIFY', value: 'true') ],),
                containerTemplate(name: 'maven', image: 'maven:3.6.0-jdk-8-alpine', ttyEnabled: true, command: 'cat')
   ],
         volumes: [
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
