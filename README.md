## AWS Amplify Vue.js Starter Template

This repository provides a starter template for creating applications using Vue.js and AWS Amplify, emphasizing easy setup for authentication, API, and database capabilities.

## Overview

This application demonstrates how to use Amplify to handle auth, appsync, and call backend lambda functions. This application has been secured via Amplify auth and is able to call the Amazon Bedrock Api and Google Gemini API. 

## Installation Steps
git clone {repo} {directory}
cd {directory}
npm install

npx ampx sandbox secret set API_KEY // Google Gemini API Key
npx ampx sandbox 
npm run dev

## Secrets Needed
API_KEY = GOOGLE_GEMINI_API_KEY

## To follow lambda logs by name
aws logs tail /aws/lambda/{functionName} --follow

## License

This library is licensed under the MIT-0 License. See the LICENSE file.

## Action Items: 
- [ ] Update the text area with the value of the to-do

## You can list all non-deleted stacks
aws cloudformation list-stacks --query 'StackSummaries[?StackStatus!=`DELETE_COMPLETE`].[StackName]' --output text

## You can create a bash script to follow all logs from a 
stack. 

#!/bin/bash

STACK_NAME="YOUR_STACK_NAME"

# Get all Lambda function resources from the stack
LAMBDA_RESOURCES=$(aws cloudformation describe-stack-resources --stack-name $STACK_NAME --query "StackResources[?ResourceType=='AWS::Lambda::Function'].PhysicalResourceId" --output text)

# For each Lambda function, tail its logs
for FUNCTION_NAME in $LAMBDA_RESOURCES
do
    echo "Tailing logs for $FUNCTION_NAME"
    aws logs tail /aws/lambda/$FUNCTION_NAME --follow &
done

# Wait for all background processes
wait








