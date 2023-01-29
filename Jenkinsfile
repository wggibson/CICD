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
      environment {
           My_User_Credentials = credentials('0a730426-f963-408f-9c8b-6d3bdbc1bbe3')
         }
      steps {
        echo "${DEVENV}"
        //echo "My Credentials are $CREDENTIALS"
        
        echo "My username is $My_User_Credentials_USR"
        echo "My password is $My_User_Credentials_PSW"

        //snApplyChanges(appSysId: "${APPSYSID}", branchName: "${BRANCH}", url: "${DEVENV}", credentialsId: "${DEV_CREDENTIALS}")
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
        echo "${TESTENV}"
        echo "My Credentials are $TEST_CREDENTIALS"
        //snInstallApp(credentialsId: "${TEST_CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}")
        //snRunTestSuite(credentialsId: "${TEST_CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
        //snRunTestSuite apiVersion: '', browserName: '', browserVersion: '', credentialsId: '', osName: '', osVersion: '', testSuiteName: '', testSuiteSysId: '', url: '', withResults: false
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
