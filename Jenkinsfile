#!/usr/bin/env groovy


node() {
    def isSuccsess = true
    def REVISION
    def TAG

    try {
        stage('Checkout') {
            deleteDir() // Workdir cleanup
            def scmVars = checkout scm

            REVISION = scmVars.GIT_COMMIT
            BRANCH = scmVars.GIT_BRANCH.take(128-"-${REVISION[0..7]}-${BUILD_NUMBER}".length()) // 128 max tag name
            BRANCH = scmVars.GIT_BRANCH.replace("/", "_")
            TAG = "${BRANCH}-${REVISION[0..7]}-${BUILD_NUMBER}"
            GIT_TAG = sh(returnStdout: true, script: "git tag --contains").trim()

            println("Branch: ${BRANCH}")
            println("Git Tag: ${GIT_TAG}")
            println("Git TAG_NAME: ${env.TAG_NAME}")
            
        }
    } catch (ex) {
        isSuccsess = false
        currentBuild.result = 'FAILURE'
    }

    finally {
       println("Pipeline finished")
    }

}

