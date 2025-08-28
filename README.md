# Salesforce Deployment

This repo helps to deploy your components to any Salesforce Orgs
## Features

- Support deployment to any Salesforce org
- Support all Unit Test Execution Levels
- Put comment after deployment successful


## How to Use

- Authorize your Salesforce org using VS Code or any cli support editor
![Authorize](https://i.ibb.co/0pLZhTMt/Screenshot-2025-08-28-at-14-11-17.png)
- Use below command in cmd to fetch **SFDX Auth URL**
```bash
sf org display --verbose
```
![SFDX AUTH URL](https://i.ibb.co/C5PTXYkY/Screenshot-2025-08-28-at-14-12-32.png)
- Copy and POST **SFDX Auth URL** to the workers by using below command in the cmd to get a token which you need to put it in the Pull Request body later
```bash
curl -X POST https://salesforce-deployment-middleware.wisnuwardana-adimas.workers.dev/generate ^
-H "Content-Type: application/json" ^
-d "{\"authUrl\":\"REPLACE_THIS_WITH_YOUR_SFDX_AUTH_URL\"}"
```
![TOKEN](https://i.ibb.co/KpzcJDRW/Screenshot-2025-08-28-at-22-41-31.png)
- Clone this repo, create new branch, push components to the branch, and lastly create Pull Request with below template put them in the PR's body description
```bash
token: REPLACE_THIS_WITH_YOUR_TOKEN
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
