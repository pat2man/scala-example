#!groovy

node ('scala') {
    def appName="scala-example-app"
    def project="jenkins-test"

    stage('Checkout') {
        echo "Checkout out from Git"
        checkout scm
    }

    stage('Compile') {
        echo 'Compiling'
        sh './sbt stage'
    }

    stage('Test') {
        echo 'Running tests'
        sh './sbt test'
        step([$class: 'JUnitResultArchiver', testResults: 'target/test-reports/*.xml'])
    }

    stage('Trigger Build') {            
        echo 'Triggering build of ${appName} in ${project}'
        sh "oc start-build ${appName} --from-dir=target/universal/stage --follow -n ${project}"
    }
}