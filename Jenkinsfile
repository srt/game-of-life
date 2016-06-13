node {

 stage 'Checkout'

 checkout scm

 stage 'compile'

 def mvnhome = tool 'M3'
 sh "${mvnhome}/bin/mvn -B compile"

 stage 'test'

 sh "${mvnhome}/bin/mvn -B -Dmaven.test.failure.ignore verify"

 step([$class: 'ArtifactArchiver', artifacts: 'gameoflife-web/target/*.war'])
 step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
 step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: '**/target/checkstyle-result.xml'])
 step([$class: 'PmdPublisher', pattern: '**/target/pmd.xml'])
}
