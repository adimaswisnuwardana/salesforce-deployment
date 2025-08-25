# Salesforce Deployment

This repo helps to deploy your components to any Salesforce Orgs
## Features

- Support deployment to any Salesforce org
- Support all Unit Test Execution Levels
- Auto close PR
- Display error message upon error


## How to Use

- Authorize your Salesforce org using VS Code or any cli support editor and fetch **SFDX Auth URL** using sf cli
```bash
sf org display --verbose
```
- POST **SFDX Auth URL** to the workers to get a token which you need to put in the Pull Request body by using cmd cli
```bash
curl -X POST https://salesforce-deployment-middleware.wisnuwardana-adimas.workers.dev/generate ^
-H "Content-Type: application/json" ^
-d "{\"authUrl\":\"force://PlatformCLI::5Aep861TSESvWeug_zXv8B3Dafez...\"}"
```
- Create Pull Request and put below template in the PR's body description
```bash
token: 123asdsampletoken
target: sandbox/production
testlevel: RunSpecifiedTests
testclass: MyTest1,MyTest2
```


## Salesforce Unit Test Execution Levels (testlevel)

**NoTestRun**

This level runs no tests during the deployment. It is only allowed for deployments to development environments like sandboxes or developer edition orgs.

**RunLocalTests**

This level runs all local Apex tests within your organization, excluding tests that originate from installed managed packages. This is the default behavior for deployments to production environments when Apex components are included in the deployment.

**RunAllTestsInOrg**

This level runs all Apex tests in your organization, including those from managed packages. This is the most comprehensive test level and is often used for critical deployments or when a full validation of the entire org's Apex code is required. 

**RunSpecifiedTests**

This level allows you to specify a list of individual test classes to run. This is useful for targeted testing of specific functionalities or when you want to quickly validate changes to a particular set of classes.