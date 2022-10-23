pipeline {
  agent any
  environment {
    APPSYSID = '73146993975b4110059ab4b3f153afae'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS = 'a199ebb1-14fa-4b09-af87-002e1420349a'
    DEVENV = 'https://dev121898.service-now.com/'
    TESTENV = 'https://dev16887.service-now.com/'
    /* PRODENV = 'https://prodinstance.service-now.com/' **/
    TESTSUITEID = 'd23d977097315510ba0d7e121153afd7'
  }
  stages {
    stage('Build') {
      /*when {
        not {
          branch 'master'
        }
      }*/
      steps {
        echo "${DEVENV}"
        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        snPublishApp(credentialsId: "${CREDENTIALS}", appSysId: "${APPSYSID}", obtainVersionAutomatically: true, url: "${DEVENV}")
      }
      
    }
    stage('Test') {
      /*when {
        not {
          branch 'master'
        }
      }*/
      steps {
        echo "${DEVENV}"
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}")
        snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
      }
    }
    /*stage('Deploy to Prod') {
      when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}")
      }
    }*/
  }
}
