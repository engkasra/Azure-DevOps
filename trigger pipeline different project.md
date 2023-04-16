My main Pipeline is in Project A with two stages:

```bash
trigger:
- none

pool:
  vmImage: ubuntu-latest

stages:

    - stage: A
      displayName: A stage
      jobs:
      - job: A
        displayName: A
        steps:
          - task: TriggerBuild@4
            inputs:
              definitionIsInCurrentTeamProject: false
              tfsServer: '{Org URL}'
              teamProject: '{Project B Name}'
              buildDefinition: '213'
              queueBuildForUserThatTriggeredBuild: false
              ignoreSslCertificateErrors: false
              useSameSourceVersion: false
              useCustomSourceVersion: false
              useSameBranch: false
              waitForQueuedBuildsToFinish: false
              storeInEnvironmentVariable: false
              authenticationMethod: 'Personal Access Token'
              password: '{PAT}'
              enableBuildInQueueCondition: false
              dependentOnSuccessfulBuildCondition: false
              dependentOnFailedBuildCondition: false
              checkbuildsoncurrentbranch: false
              failTaskIfConditionsAreNotFulfilled: false
    
    - stage: B
      displayName: B stage
      dependsOn: A
      jobs:
      - job: 
        steps:
        - bash: echo "B"
 ```
