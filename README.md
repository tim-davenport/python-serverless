# Flask example running in Lambda using the Serverless Framework

## Setting things up
You will need:
- Node & NPM
- Python, PIP and virtualenv
- [AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-install.html) installed and configured

Now, install the serverless framework:
`npm install serverless -g`

Then, install the other packages required for this demo:
`npm install`

Create and then activate the Python virtual environment:
```
python3 -m venv env
source env/bin/activate
```

Install the required PIP packages:
```
python3 -m pip install -r requirements.txt
```

At this point, you should be able to emulate and run a Serverless Lambda environment locally with `sls wsgi serve`

Open the URL from the output, and you should see the 'Hello World' response.

## Deployment to AWS Lambda

Before you can deploy this demo to Lambda, you will need the ID of the API Gateway REST API and it's root resource from the AWS console. If you haven't got one, just create one in the AWS console - you don't need to define any resources or other settings. You could also use CloudFormation or Terraform to deploy an API Gateway so if that's the case grab their Ids. Refer to [this link](https://github.com/serverless/serverless/blob/master/docs/providers/aws/events/apigateway.md#manually-configuring-shared-api-gateway) to help identify what you need to plug into this section of the `serverless.yml` in the root of this demo:

```
apiGateway:
    restApiId: <enter yours here>
    restApiRootResourceId: <enter yours here>
```

Then, assuming the AWS CLI is installed and configured with a profile (run `aws configure` if you haven't done this already and refer to the AWS docs), you can deploy the Flask application to Lambda with `sls deploy`

Once it's finished, copy and paste the URL from the output into a browser and you should see the 'Hello World' response being served from AWS API Gateway and Lambda.

## Useful Links

[How to convert an existing Flask app to a Serverless app](https://www.serverless.com/blog/flask-python-rest-api-serverless-lambda-dynamodb#converting-an-existing-flask-application)

[The wsgi plugin for Serverless (maps between API Gateway/Lambda and wsgi)](https://pypi.org/project/serverless-wsgi/)

[Why this won't work with Flask 2.x - only 1.1.4 for the time being](https://github.com/UnitedIncome/serverless-python-requirements/issues/469)

