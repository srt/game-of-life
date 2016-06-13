node {

 stage 'Checkout'

 git url: 'https://github.com/srt/game-of-life.git'

 stage 'compile'

 def mvnhome = tool 'M3'
 sh "${mvnhome}/bin/mvn -B compile"

 stage 'test'

 sh "${mvnhome}/bin/mvn -B -Dmaven.test.failure.ignore verify"

 input message: "Does http://localhost:8888/staging/ look good?"

        step([$class: 'ArtifactArchiver', artifacts: 'gameoflife-web/target/*.war'])
        step([$class: 'WarningsPublisher', consoleParsers: [[parserName: 'Maven']]])
        step([$class: 'JUnitResultArchiver', testResults: '**/target/surefire-reports/TEST-*.xml'])
        step([$class: 'JavadocArchiver', javadocDir: 'gameoflife-core/target/site/apidocs/'])
        step([$class: 'hudson.plugins.checkstyle.CheckStylePublisher', pattern: '**/target/checkstyle-result.xml'])
        // In real life, PMD and Findbugs are unlikely to be used simultaneously
        step([$class: 'PmdPublisher', pattern: '**/target/pmd.xml'])
        step([$class: 'AnalysisPublisher'])

}
