pipeline {
  agent any
  environment {
    APPSYSID = '73146993975b4110059ab4b3f153afae'
    BRANCH = "${BRANCH_NAME}"
    CREDENTIALS = '7f324017-02b1-4d1e-b565-d7ef882356be'
    DEV_CREDENTIALS = '7f324017-02b1-4d1e-b565-d7ef882356be'
    TEST_CREDENTIALS = '7f324017-02b1-4d1e-b565-d7ef882356be'
    DEVENV = 'https://dev121898.service-now.com/'
    TESTENV = 'https://dev16887.service-now.com/'
    /* PRODENV = 'https://prodinstance.service-now.com/' **/
    TESTSUITEID = 'd23d977097315510ba0d7e121153afd7'
  }
  stages {
    stage('Validated User Name') {
      steps {
        //echo "${CREDENTIALS}"
        echo "My Credentials are ${CREDENTIALS}"
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
        echo "${BRANCH}"

        snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${DEV_CREDENTIALS}")
        //snPublishApp(credentialsId: "${CREDENTIALS}", appSysId: "${APPSYSID}", isAppCustomization: true, obtainVersionAutomatically: true, url: "${DEVENV}")
        //snRunTestSuite(credentialsId: "${CREDENTIALS}", url: "${DEVENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
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
        echo "Installing on ${TESTENV}"

        snInstallApp(credentialsId: "${TEST_CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}")
        //snRunTestSuite(credentialsId: "${TEST_CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
        //snRunTestSuite apiVersion: '', browserName: '', browserVersion: '', credentialsId: '', osName: '', osVersion: '', testSuiteName: '', testSuiteSysId: '', url: '', withResults: false
      }
    }
    stage('Deploy to Prod') {
      echo "########### Ready to deploy to PROD ###########"
      /*when {
        branch 'master'
      }
      steps {
        snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}")
      }*/
    }
  }
}
