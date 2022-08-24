# Is this review primarily based on AWS Cloud Resources?
### ["Yes","No"]
## Does your application adhere to all must haves in the Must Haves Should Dos?  If not, please identify areas you are non-compliant.
### ["Yes"]
## Which environments/accounts is this project expected to utilize?
### ["dev-private","dev","test","stage","OTE","production"]
## Is everything you are using in ADOPT or MAINTAIN on TechRadar?  If not, please identify methods or technologies not in ADOPT or MAINTAIN.
### ["Yes"]
## Is all sensitive information, e.g. credentials, keys, certs, etc, stored inside of AWS Secrets Manager or AWS Certificate Manager?
### ["Yes"]
## Will application security logging be included for your production services prior to taking production traffic?
### ["Yes"]
## Which of the following strategies do you apply for least privilege and zero trust?
### ["WAF/Firewall manager allow lists","AUTHZ enforcement per endpoint"]
## Will there be any admin access to any production resource beyond Break-Glass Procedure?
### ["Yes","No"]
## Is there a method of accessing production resources beyond Escalating Privileges?
### ["Yes","No"]
## Do all deployments in this project automatically generate change orders when deploying to production per the Global Change Management Policy?
### ["Yes"]
## Please describe all end users of this project:
### ["Employees","Shopper Customers","Turnkey Resellers","API Resellers","PASS Users","Delegations"]
## Select all authentication systems the project is using:
### ["Okta","GoDaddy's Identity Auth Platform","Collect/Process/Store auth creds within this system"]
## Will employees access any services in this project as an internal tool?
### ["Yes","No"]
### Do all tools hosted in this account adhere to the Tool Security Standard in full?
#### ["Yes"]
## Are any services within this project a Service Tier 0 or 1?
### ["Yes","No"]
### Which regions will this project utilize? Select all that apply:
#### ["ap-southeast-2","ap-south-1","ap-southeast-1","ap-northeast-3","ap-northeast-2","ap-northeast-1","ca-central-1","eu-west-1","eu-west-2","eu-central-1","eu-west-3","sa-east-1","us-east-1","us-west-2","us-east-2","us-west-1","cn-north-1","cn-northwest-1"]
### Is your application integrated with SPAQ to capture application metrics?
#### ["Yes"]
### How are you proving your Business Continuity and Disaster Recovery Plan?
#### ["Load Testing","Stress Testing","Chaos Engineering","Game Days"]
### Which of the following automated tests are required to pass within your CICD pipelines prior to deployment? Select all that apply:
#### ["Vulnerability scans","Fuzz testing","Unit testing","Integration testing","Compliance testing","Code coverage"]
### Which methods would be used in this project to double/half capacity?
#### ["Auto Scaling","Gated Scaling","Manual Scaling"]
## Do you process, store, transmit or impact the security of data in your service?
### ["Yes","No"]
### Are all datastores compliant with all appropriate data retention policies?
#### ["Yes"]
### Is there a process in place to delete data that exceeds retention periods on at least a quarterly basis?
#### ["Yes"]
### Is administrative access to the datastore disallowed by policy?
#### ["Yes"]
### Is data ever moved from Prod to Non-Prod environments?
#### ["Yes","No"]
#### For what purposes are data moved from Prod to Non-Prod environments?
##### ["Model Training","Testing"]
### Does your application store, process, transmit or impact the security of P*I data?
#### ["Yes","No"]
#### Sensitive or P*I Data must be application layer encrypted. Please select which method you are using:
##### ["TDE","Data Layer","Asherah","App Layer","Custom"]
#### Is there a process to securely delete PII data upon request?
##### ["Yes"]
#### How are you monitoring for unauthorized transfer of sensitive and/or P# I information across the network?
##### ["ESSP"# "CloudWatch logs"]
## Does your service publicly expose any service, UI or endpoints outside of this project?
### ["Yes","No"]
### Which of the following are configured for static content deliver?
#### ["CDN Cloudfront","CDN Sucuri","CDN Akamai"]
### Which of the following are configured to protect the exposed interfaces?
#### ["WAF AWS","WAF Sucuri","WAF Akamai Kona"]
### Select all domains this application will run on:
#### ["godaddy.com","gdcorp.tools","gd3p.tools","secureserver.net","int.godaddy.com","int.gdcorp.tools","int.gd3p.tools","int.secureserver.net"]
## Will this project be using machine learning before your next readiness review?
### ["Yes","No"]
### Do you have documented training data?
#### ["Yes"]
### Which interactive notebooks are you using?
#### ["Jupiter","Sagemaker"]
### What is the code coverage for the data generation code?
#### ["25% or less","50%","75%","greater than 90%"]
### Do you automatically retrain each model?
#### ["Yes"]
### Do you automatically redeploy retrained models?
#### ["Yes"]
### What is your test coverage of model usage?
#### ["Unit Tests","Integration Tests"# "End to End Tests","None"]
# Is this review primarily based on on-prem resources?
### ["Yes","No"]
## Does your application adhere to all must haves in the Must Haves Should Dos?  If not, please identify areas you are non-compliant.
### ["Yes"]
## Do you have a plan to migrate to AWS within the next 12 months?
### ["Yes"]
## Have all components been constructed in compliance with GoDaddy Software Development Policy?  If not, please identify areas you are non-compliant.
### ["Yes"]
## Is everything you are using in ADOPT or MAINTAIN on TechRadar?  If not, please identify methods or technologies not in ADOPT or MAINTAIN.
### ["Yes"]
## Do all deployments in this project automatically generate change orders when deploying to production?
### ["Yes"]
## Is all user access to servers managed by AD?
### ["Yes"]
## Reusable deployment artifacts are stored in:
### ["Artifactory","Yum"]
## Is all sensitive information, e.g. credentials, keys, certs, etc, stored inside of AWS Secrets Manager?
### ["Yes"]
## Which active agent is installed on each server to report on OS and package updates?
### ["Tanium","patchmon"]
## Which active agent is installed on each server to perform OS and package updates?
### ["Salt","Chef","Puppet","Ansible"]
## Is security logging applied to all systems?
### ["Yes"]
## Will application security logging be included for your production services?
### ["Yes"]
## Please describe all end users of this project:
### ["Employees","Shopper Customers","Turnkey Resellers","API Resellers","PASS Users","Delegations"]
## Select all authentication systems the project is using:
### ["Okta","GoDaddy's Identity Auth Platform","Collect/Process/Store auth creds within this system"]
## Will employees access this service as an internal tool?
### ["Yes","No"]
### Do all tools hosted in this account adhere to the Tool Security Standard in full?
### ["Yes"]
## Is your service a Service Tier 0 or 1?
### ["Yes","No"]
### Which datacenters or colocations will this project utilize?
### ["P3","IAD","SIN","AMS"]
### Is your application integrated with the SPAQ platform to capture application metrics?
### ["Yes"]
### Which of the following automated tests are required to pass within your CICD pipelines prior to deployment?
#### ["Vulnerability scans","Fuzz testing","Unit testing","Integration testing","Compliance testing","Code coverage"]
## Do you process, store, transmit or impact the security of data in your service?
### ["Yes","No"]
### Is data ever moved from Prod to Non-Prod environments?
### ["Yes","No"]
#### For what purposes are data moved from Prod to Non-Prod environments?
#### ["Model Training","Testing"]
### Are all datastores compliant with all appropriate data retention policies?
### ["Yes"]
### Is there a process in place to delete data that exceeds retention periods on at least a quarterly basis?
### ["Yes"]
### Is administrative access to the datastore disallowed by policy?
### ["Yes"]
### Is data ever moved from Prod to Non-Prod environments?
#### ["Yes","No"]
#### For what purposes are data moved from Prod to Non-Prod environments?
##### ["Model Training","Testing"]
### Does your application store, process, transmit or impact the security of P*I data?
#### ["Yes","No"]
#### Sensitive or P*I Data must be application layer encrypted. Please choose which method you are using to do so
##### ["TDE","Data Layer","App Layer","Asherah","Custom"]
#### Is there a process to securely delete PII data upon request?
##### ["Yes"]
#### How is P*I data encrypted at rest?
##### ["Database encryption","Application encryption]
## Does your service publicly expose any service, UI or endpoints outside of this project?
### ["Yes","No"]
### Select all domains this application will run on:
### ["godaddy.com","gdcorp.tools","gd3p.tools","secureserver.net","int.godaddy.com","int.gdcorp.tools","int.gd3p.tools","int.secureserver.net"]
### Which of the following are configured for static content deliver?
### ["CDN Akamai"]
### Which of the following are configured to protect the exposed interfaces?
### ["WAF Sucuri","WAF Akamai Kona"]
## Will this project be using machine learning before your next readiness review?
### ["Yes","No"]
### Do you have documented training data?
### ["Yes"]
### Which interactive notebooks are you using?
### ["Jupiter","Sagemaker"]
### What is the code coverage for the data generation code?
### ["25% or less","50%","75%","greater than 90%"]
### Do you automatically retrain each model?
### ["Yes"]
### Do you automatically redeploy retrained models?
### ["Yes"]
### What is your test coverage of model usage?
### ["Unit Tests","Integration Tests"# "End to End Tests","None"]

### What changes could we make to this readiness review process to improve it?####