def gitTag = null

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
  
  parameters {
    snParam(credentialsForPublishedApp: "${CREDENTIALS}", instanceForPublishedAppUrl: "${DEVENV}", sysId: "${APPSYSID}", appScope: "x_739109_cicd_demo", publishedAppVersion: "1.0.7")
  }
  stages {
    stage('Validated User Name') {
      steps {
        //echo "${CREDENTIALS}"
        echo "My Credentials are ${CREDENTIALS}"
      }
    }
    
    stage('Buil Preparation') {
      steps {
        echo "${DEVENV}"
        echo "${BRANCH}"    
        
        // run your build scripts
       // checkout scm
        //sh 'npm --version'
        //sh 'npm install'
        //sh 'grunt dev-setup --no-color'
        
        script {
          gitTag=sh(returnStdout: true, script: "git tag --contains | head -1").trim()
        }
        echo "${params.snParam}" // for debugging
        
        snApplyChanges()

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
      when {
        expression {
          return gitTag;
        }
      }
      steps {
        echo "Installing on ${TESTENV}"

        snInstallApp(credentialsId: "${TEST_CREDENTIALS}", url: "${TESTENV}", appSysId: "${APPSYSID}")
        //snRunTestSuite(credentialsId: "${TEST_CREDENTIALS}", url: "${TESTENV}", testSuiteSysId: "${TESTSUITEID}", withResults: true)
        //snRunTestSuite apiVersion: '', browserName: '', browserVersion: '', credentialsId: '', osName: '', osVersion: '', testSuiteName: '', testSuiteSysId: '', url: '', withResults: false
      }
    }
    stage('Deploy to Prod') {
      /*when {
        branch 'master'
      }*/
      steps {
        echo "########### Ready to deploy to PROD ###########"
        //snInstallApp(credentialsId: "${CREDENTIALS}", url: "${PRODENV}", appSysId: "${APPSYSID}")
      }
    }
  }
}
