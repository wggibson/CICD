pipeline {
  agent any
  environment {
    APPSYSID = '73146993975b4110059ab4b3f153afae'
    BRANCH = "${BRANCH_NAME}"
    NOW_CREDENTIALS = credentials('268e2e76-d3b1-4032-a9a1-79955fa9b5b6')
    //NOW_CREDENTIALS = credentials('eugene.sikorski:!Marines123')
    DEVENV = 'https://dev121898.service-now.com/'
    TESTENV = 'https://dev16887.service-now.com/'
    /* PRODENV = 'https://prodinstance.service-now.com/' **/
    TESTSUITEID = 'd23d977097315510ba0d7e121153afd7'
  }
  stages {
    stage('Validated User Name') {
      steps {
        echo "${NOW_CREDENTIALS}"
        //sh('echo ${NOW_CREDENTIALS}')
      }
    }
    
    stage('Build') {
      /*when {
        not {
          branch 'master'
        }
      }*/
      steps {
        echo "${DEVENV}"
        //snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${CREDENTIALS}")
        //snPublishApp(credentialsId: "${CREDENTIALS}", appSysId: "${APPSYSID}", obtainVersionAutomatically: true, url: "${DEVENV}")
        snRunTestSuite(credentialsId: "${NOW_CREDENTIALS}", url: "${DEVENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
        //snRunTestSuite apiVersion: '', browserName: '', browserVersion: '', credentialsId: '', osName: '', osVersion: '', testSuiteName: '', testSuiteSysId: '', url: '', withResults: false
      }
      
    }
    stage('Test') {
      /*when {
        not {
          branch 'master'
        }
      }*/
      steps {
        echo "${TESTENV}"
        /*snInstallApp(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}")
        snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)*/
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
