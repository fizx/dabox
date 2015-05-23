Dabox is a RESTful API Server that operates over AWS Lambda.  It's optimized for allowing arbitrary users to upload and execute very small, fast code snippets in individual sandboxes.  The sandbox will have access to the open internet, but no access to anything inside your AWS account.

Dabox is deployed as a CloudFormation template.  Just upload the cf.json file at the appropriate point in the aws control panel workflow, or use the one-click installer here (TBD).  To clean up, delete the CloudFormation instance.

As the only pre-requisite for this process, you should have a (possibly self-signed) SSL Certificate, and you should know its ARN.  On a Mac, this looks like (replace the text in brackets):

    :$ brew install aws-iam-tools
    :$ openssl req -new -key ~/.ssh/[some-keypair].pem -out csr.pem
    :$ openssl x509 -req -days 3650 -in csr.pem -signkey ~/.ssh/[some-keypair].pem -out server.crt
    :$ iam-servercertupload -b server.crt -s [some-cert-name] -k ~/.ssh/[some-keypair].pem
    :$ iam-servercertgetattributes -s [some-cert-name] | head -1        # Outputs the ARN
