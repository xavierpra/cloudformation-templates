# Static Website
The template [static-website.yaml](static-website.yaml) provides configuration for setting up AWS services for hosting a static website.

## Prerequisites
The template automatically creates the appropriate DNS record in Route 53 for associating the CloudFront distribution with your domain. Therefore, it is necessary to provide the ID of the Hosted Zone as a parameter. The Hosted Zone can either be created manually of via the CloudFormation template [hosted-zone.yaml](../dns/hosted-zone.yaml).

Additionally, the template configures an ACM certificate which is used to enable SSL encrypted connections to the CloudFront distribution. The validation of the certificate is performed by adding CNAME records to the DNS configuration of the domain.

## Setup
The following AWS CLI command can be used to launch the infrastructure:

```
aws cloudformation create-stack --stack-name my-static-website \
                                --template-body file://static-website.yaml  \
                                --parameters ParameterKey=HostedZoneId,ParameterValue=Z2CV1LKAQAGQWM \
                                             ParameterKey=DomainName,ParameterValue=www.example.com \
                                --region us-east-1
```

It is important to launch the infrastructure in the region "N. Virginia" (us-east-1) since CloudFront can only work with ACM certificates provisioned in this region.
