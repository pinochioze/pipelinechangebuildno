#!/usr/bin/env groovy
node {
  stage('JIRA') {
/*
    triggers{
      bitbucketpr(projectPath:'<BIT_BUCKET_PATH>',
      cron:'H/15 * * * *',
      credentialsId:'',
      username:'',
      password:'',
      repositoryOwner:'',
      repositoryName:'',
      branchesFilter:'',
      branchesFilterBySCMIncludes:false,
      ciKey:'',
      ciName:'',
      ciSkipPhrases:'',
      checkDestinationCommit:false,
      approveIfSuccess:false,
      cancelOutdatedJobs:true,
      commentTrigger:'')
    }
*/
    checkout([$class: 'GitSCM', 
//            branches: [[name: "*/prforpipeline"]], 
            branches: [[name: "${sha1}"]],
          extensions: [[$class: 'LocalBranch']], 
   userRemoteConfigs: [[refspec: "+refs/pull/*:refs/remotes/origin/pr/*", 
                 url: "https://github.com/pinochioze/pipelinechangebuildno.git"

                      
                      ]]])


//    def searchResults = jiraJqlSearch jql: "project = ProjectManagement AND issuekey = 'HVC-10'"
//    def issues = searchResults.data.issues
//    sh 'env'

    println '===================== GET SERVER INFO ====================================================='
    withEnv(['JIRA_SITE=JiraLocal']) {
      def serverInfo = jiraGetServerInfo()
      echo serverInfo.data.toString()
    }

    def searchResults = jiraJqlSearch jql: 'PROJECT = ProjectManagement', site: 'JiraLocal', failOnError: true
//    def issues = searchResults.data.issues
//    echo searchResults.data.toString()
//    echo searchResults.data.issues.toString()
    echo searchResults.data.issues.size().toString()
    

    println '===================== GET INFO from HVC-7 issue  =========================================='
    def issue = jiraGetIssue idOrKey: 'HVC-7', site: 'JiraLocal'
//    echo issue.data.toString()


    println '===================== EDIT DESCRIPT on HVC-7 issue  ======================================='
    def testIssue = [fields: [ project: [id: '10000'],
                           summary: 'New JIRA Created from Jenkins.',
                           description: '||No||PR||Commit||UnitTest||FunctionTest||PerfTest||Note||\n|l|PR-1|abcdefghijklm|Passed|Passed|Passed| |\n|2|PR-2|abcdefghijklm|Passed|Passed|Passed| |\n|3|PR-3|abcdefghijklm|Passed|Passed|Passed| |'
                           ]]
    response = jiraEditIssue idOrKey: 'HVC-7', issue: testIssue, site: 'JiraLocal'
//    echo response.successful.toString()
//    echo response.data.toString()


    println '===================== GET COMMENT IN HVC-7  =============================================='
    def comment = jiraGetComment site: 'JiraLocal', idOrKey: 'HVC-7', commentId: '10006'
    echo comment.data.toString()
    

    println '===================== GET ALL COMMENTS IN HVC-7  ======================================== '
    def comments = jiraGetComments site: 'JiraLocal', idOrKey: 'HVC-7'
    comments = jiraGetComments site: 'JiraLocal', idOrKey: 'HVC-7'
    echo comments.data.toString()
    
    println '===================== EDIT COMMENTS IN HVC-7  ======================================== '
    comment = [ body: '||No||PR||Commit||UnitTest||FunctionTest||PerfTest||Note||\n|l|PR-10|qwertyuiopasd|Passed|Passed|Passed| |\n|2|PR-20|abcdefghijklm|Passed|Passed|Passed| |\n|3|PR-30|abcdefghijklm|Passed|Passed|Passed| |' ]
    jiraEditComment site: 'JiraLocal', idOrKey: 'HVC-7', commentId: '10001', input: comment





    println '===================== GET FIELD IN HVC-7  ================================================='
//    def fields = jiraGetFields idOrKey: 'HVC-7', site: 'JiraLocal'
//    echo fields.data.toString()


//    println '===================== GET ALL COMMENTS IN HVC-7  =========================================='
//    comments = jiraGetComments site: 'JiraLocal', idOrKey: 'HVC-7'
//    echo comments.data.toString()


    println '===================== ADD COMMENTS IN HVC-7  =========================================='
    comment = [ body: 'test comment' ]
//    jiraAddComment site: 'JiraLocal', idOrKey: 'HVC-7', input: comment










    echo "BUILD_NUMBER: ${BUILD_NUMBER}"
//    echo "GIT_COMMIT: ${GIT_COMMIT}"

    echo "sha1: ${sha1}"
    echo "BUILD_TAG: ${BUILD_TAG}"
    echo "BUILD_ID: ${BUILD_ID}"
    echo "EXECUTOR_NUMBER: ${EXECUTOR_NUMBER}"
    BUILD_NUMBER = sha1
    echo "BUILD_NUMBER: ${BUILD_NUMBER}"


//    println '===================== MODIFY COMMENT IN HVC-7  ============================================'
//    def comment = [body: 'test comment', visibility: [type: 'role', value: 'Developer' ]]
//    def comment = [ body: 'test comment' ]
//    jiraEditComment site: 'JiraLocal', idOrKey: 'HVC-7', commentId: '10002', input: comment


/*

    println '===================== GET ISSUELINK IN HVC-7 =============================================='
    def issueLink = jiraGetIssueLink id: '10000', site: 'JiraLocal', failOnError: false
    echo issueLink.data.toString()



    println '===================== GET ISSUELINK TYPE IN HVC-7 ========================================='
    def issueLinkTypes = jiraGetIssueLinkTypes site: 'JiraLocal', failOnError: false
    echo issueLinkTypes.data.toString()



    println '===================== ADD CUSTOM FIELD = DEVELOPMENT ======================'
    def testIssue = [fields: [ project: [id: '10000'],
                           summary: 'New JIRA Created from Jenkins.',
                           description: 'New JIRA Created from Jenkins.',
                           
                           issuetype: [id: '3']]]

    response = jiraEditIssue idOrKey: 'HVC-7', issue: testIssue, site: 'JiraLocal'
    echo response.successful.toString()
    echo response.data.toString()
*/
    

/*

    for (i = 0; i <issues.size(); i++) {
      def fixVersion = jiraNewVersion version: [name: "new-fix-version-1.0", project: "ProjectManagement"]
      def testIssue = [fields: [fixVersions: [fixVersion.data]]]
      response = jiraEditIssue idOrKey: issues[i].key, issue: testIssue
    }
*/

  }
}
