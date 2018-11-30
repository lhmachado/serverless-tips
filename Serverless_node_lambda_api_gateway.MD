# Serverless with NodeJS Lambda + API Gateway

## We will use

- [Serverless Framework](https://serverless.com/)
- [AWS Lambda](https://aws.amazon.com/lambda/)
- [AWS API Gateway](https://aws.amazon.com/pt/api-gateway/)
- [NodeJS](https://nodejs.org/en/)

## Pre-requisites

- Installed [node 8](https://nodejs.org/dist/latest-v8.x/) latest stable version.
- An aws working account.

## Installation

- [Install serverless framework guide](https://serverless.com/framework/docs/providers/aws/guide/installation/)

Shortchut:

```bash
 npm install -g serverless
 serverless
 serverless --version
```

Run again to update:

```bash
npm install -g serverless
```

- [Setting up aws credentials](https://serverless.com/framework/docs/providers/aws/guide/credentials/)

Shortcut:

```bash
export AWS_ACCESS_KEY_ID=<your-key-here>
export AWS_SECRET_ACCESS_KEY=<your-secret-key-here>
```

## Creating a nodejs project

```
    sls create --template aws-nodejs --path <projectname>
```

Result expected:

```
Serverless: Generating boilerplate...
Serverless: Generating boilerplate in "~/projectname"
 _______                             __
|   _   .-----.----.--.--.-----.----|  .-----.-----.-----.
|   |___|  -__|   _|  |  |  -__|   _|  |  -__|__ --|__ --|
|____   |_____|__|  \___/|_____|__| |__|_____|_____|_____|
|   |   |             The Serverless Application Framework
|       |                           serverless.com, v1.33.2
 -------'

Serverless: Successfully generated boilerplate for template: "aws-nodejs"
```

Uncomment lines 64-67 like:

```yml
functions:
  hello:
    handler: handler.hello

    #    The following are a few example events you can configure
    #    NOTE: Please make sure to change your handler code to work with those events
    #    Check the event documentation for details
    events:
      - http:
          path: users/create
          method: get
```

Just deploy it:

```bash
sls deploy
```

Result must be like:

```bash
Serverless: Stack update finished...
Service Information
service: <yourservice>
stage: dev
region: us-east-1
stack: <yourfunction>-dev
api keys:
  None
endpoints:
  GET - https://<deployedid>.execute-api.us-east-1.amazonaws.com/dev/users/create
functions:
  hello: <yourfunction>-dev-hello
layers:
  None
```

Just curl your api gateway endpoint:

```bash
curl https://<deployedid>.execute-api.us-east-1.amazonaws.com/dev/users/create
```

Result expected:

```bash
{"message":"Go Serverless v1.0! Your function executed successfully!","input":{"resource":"/users/create","path":"/users/create","httpMethod":"GET","headers":{"Accept":"*/*","CloudFront-Forwarded-Proto":"https","CloudFront-Is-Desktop-Viewer":"true","CloudFront-Is-Mobile-Viewer":"false","CloudFront,TRUCATED}
```
