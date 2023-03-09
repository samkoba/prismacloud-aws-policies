Policy Details
PC-AWS-IAM-563

Policy Name
AWS SageMaker notebook instance IAM policy overly permissive to all traffic

Description(Optional)
This policy identifies SageMaker notebook instances IAM policies that are overly permissive to all traffic. It is recommended that the SageMaker notebook instances should be granted access restrictions so that only authorized users and applications have access to the service.

For more details:
https://docs.aws.amazon.com/sagemaker/latest/dg/security_iam_id-based-policy-examples.html

Policy Subtype: Run

Severity : High


Rule

AWS SageMaker notebook instance IAM policy overly permissive to all traffic_RL

Query
JSON Preview

config from cloud.resource where cloud.type = 'aws' AND api.name = 'aws-iam-get-policy-version' AND json.rule = document.Statement[?any((Condition.IpAddress.aws:SourceIp contains 0.0.0.0/0 or Condition.IpAddress.aws:SourceIp contains ::/0) and Effect equals Allow and Action anyStartWith sagemaker:)] exists





#Remediation
1. Login to AWS console
2. Goto IAM Services
3. Click on 'Policies' in left hand panel
4. Search for the Policy for which the Alert is generated and click on it
5. Under Permissions tab, click on Edit policy
6. Under the Visual editor, for each of the 'SageMaker' Service, click to expand and perform following.
6.a. Click to expand 'Request conditions'
6.b. Under the 'Source IP', remove the row with the entry '0.0.0.0/0' or '::/0'. Add condition with restrictive IP ranges.
7. Click on Review policy and Save changes.
