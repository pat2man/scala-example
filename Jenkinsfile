#!groovy

node ('scala') {
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
        echo 'Triggering build of scala-example-app in jenkins-test'
        sh "oc start-build scala-example-app --from-dir=target/universal/stage --follow -n ${project}"
    }
}