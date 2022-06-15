# rr-streamlining

``` mermaid
%%{init: { "flowchart": { "htmlLabels": true, "curve": "linear", "logLevel": 1 } } }%%
graph TD
    OnPrem{Is this project on-prem?}
    Acquisition{Is this project from an acquisition?}
    AWS{Is this project AWS based?}
    End{end}

    OnPrem --->|Yes| OPBase100
    OnPrem -->|No| Acquisition
    Acquisition --->|Yes| AcqBase100
    Acquisition -->|No| AWS
    AWS --->|Yes| AwsBase100
    AWS ---->|No| End
    OPOps102 ----> End
    AcqOps102 ----> End
    AwsML000 ---->|No| End
    AwsML806 --> End

    subgraph OnpremG [OnPremG]
      OPBase100{"We have on-prem questions for you!"}
      OPBase100 ---> OPData101
      OPData101{"We have on-prem data questions for you!"}
      OPData101 ---> OPOps102
      OPOps102{"We have on-prem Ops questions for you!"}
    end

    subgraph AcquisitionG [AcquisitionG]
      AcqBase100{"We have acquisition questions for you!"}
      AcqBase100 ---> AcqData101
      AcqData101{"We have acquisition data questions for you!"}
      AcqData101 ---> AcqOps102
      AcqOps102{"We have acquisition Ops questions for you!"}
    end

    %% AWS
    subgraph AWSG [AWSG]
      %% Should we ask:
      %% - Serverless?
      %%
      %% AWS Base Questions - No gating question.
      AwsBase100{Does your application adhere to all must haves in the Must Haves Should Dos?}
      AwsBase100 --> AwsBase101  %% Further review required
      AwsBase101{Which environments/accounts is this project expected to utilize?}
      AwsBase101 --> AwsBase102  %% Keep it!  Keep it base
      AwsBase102{Please describe all end users of this project:}
      AwsBase102 --> AwsBase103 %% Gate this with "Are there services im this account utilized by employees?""
      AwsBase103{"Is everything you are using in ADOPT on TechRadar?"}
      AwsBase103 --> AwsBase104  %% Maybe base/general
      AwsBase104{"Is security logging applied to all systems and will it include application security logging for your production services prior to taking production traffic?"}
      AwsBase104 --> AwsBase105  %% Keep - base
      AwsBase105{"Which of the following strategies do you apply for least privilege and zero trust?"}
      AwsBase105 --> AwsBase106  %% Keep
      AwsBase106{"Will there be any admin access to any production resource beyond Break-Glass Procedure?"}
      AwsBase106 --> AwsBase107  %% Keep
      AwsBase107{"How often do you upgrade your software/packages/libs or self-managed applications?"}
      AwsBase107 --> AwsBase108  %% Keep
      AwsBase108{"Are all logs, monitors, and alerts configured in compliance with 'GoDaddy Monitoring Standard', and confirmed to be operating appropriately?"}
      AwsBase108 --> AwsBase109
      AwsBase109{"Is your application integrated with the SPAQ to capture application metrics?"}
      AwsBase109 --> AwsBase110
      AwsBase110{"Have you identified recovery processes for each layer of your application?"}
      AwsBase110 --> AwsBase111  %% Keep
      AwsBase111{"Do all deployments in this project generate change orders when deploying to production?"}
      AwsBase111 --> AwsBase112  %% Keep
      AwsBase112{"Select all authentication systems the project is using:"}
      AwsBase112 --> AwsBase113  %% Keep, but gate - base
      AwsBase113{"Do all tools hosted in this account adhere to the Tool Security Standard in full?"}
      AwsBase113 --> AwsST01000  %% Keep but gate - base


      %% AWS - Service Tier 1 or 0
      AwsST01000{"Is your service a Service Tier 0 or 1?"}
      AwsST01000 -->|Yes| AwsST01001
      AwsST01000 -->|No| AwsData000
      AwsST01001{Which regions will this project utilize?}
      AwsST01001 --> AwsST01002  %% Gating questions on Service Tier 0
      AwsST01002{What is the expected maximum growth rate per month of any service in these accounts?}
      AwsST01002 --> AwsST01003  %% Gate with Service Tier 0 - combine these 3 questions into 1
      AwsST01003{What is the expected maximum burst of any service in these accounts?}
      AwsST01003 --> AwsST01004
      AwsST01004{How many concurrent users do you expect to have at peak time?}
      AwsST01004 --> AwsST01005
      AwsST01005{How are you proving your Business Continuity and Disaster Recovery Plan?}
      AwsST01005 --> AwsST01006  %% Gating questions on Service Tier 0/1
      AwsST01006{"Do your CICD pipeline(s) utilized in this project require passing build, automated, and security tests including passing any security scans with no High/Critical vulnerabilities prior to deployment?"}
      AwsST01006 --> AwsST01007  %% Service Tier 0/1
      AwsST01007{"Which methods would be used in this project to double/half capacity?"}
      AwsST01007 --> AwsData000  %% Service Tier 0/1 bucket

      %% AWS Data
      AwsData000{"Do you process or store data in your service?"}
      AwsData000 -->|Yes| AwsData002
      AwsData000 ---->|No| AwsWeb000
      AwsData002{"For what purposes is data moved from Prod to Non-Prod environments?"}
      AwsData002 --> AwsData004   %% Keep it
      AwsData004{"Are all datastores compliant with all appropriate data retention policies?"}
      AwsData004 --> AwsData005   %% Ask Brittany
      AwsData005{"Is there a process in place to delete data that exceeds retention periods on at least a quarterly basis?"}
      AwsData005 --> AwsData006   %% Ask Brittany
      AwsData006{"What is your authentication model for accessing your database?"}
      AwsData006 --> AwsData007   %% Keep it
      AwsData007{Does your application store, process, and/or transmit P* data?}
      AwsData007 -->|Yes| AwsData008
      AwsData007 ---->|No| AwsWeb000
      AwsData008{"Sensitive or P*I Data must be application layer encrypted, please choose which method you are using to do so"}
      AwsData008 --> AwsData009  %% Keep it
      AwsData009{"Is there a process to securely delete PII data upon request?"}
      AwsData009 --> AwsData010   %% Keep it
      AwsData010{"How are you monitoring for unauthorized transfer of sensitive and/or p*i information across the network? (you should evaluate your application log metadata for indications of threat actor abuse of your application)"}
      AwsData010 --> AwsWeb000



      %% AWS Web Application
      AwsWeb000{"Does your service expose any UI or endpoints outside of your AWS accounts?"}  %% Reword
      AwsWeb000 -->|Yes| AwsWeb100
      AwsWeb000 ---->|No| AwsPriv000
      AwsWeb100{How many requests per second will the most active endpoint receive?}
      AwsWeb100 --> AwsWeb101  %% DELETE all scaling related questions and defer to artifacts
      AwsWeb101{"Which of the following are used to protect the exposed interfaces?"}
      AwsWeb101 --> AwsWeb102  %% Keep it
      AwsWeb102{"Select all domains this application will run on:"}
      AwsWeb102 --> AwsWeb103  %% Keep it
      AwsWeb103{"Web applications are utilizing the following CDNs for static assets: (check all that apply)"}
      AwsWeb103 --> AwsPriv000  %% Keep for now - further review.  Maybe move to on-prem and acq


      %% Privacy and Compliance
      AwsPriv000{"NEED GATING QUESTION - Do you have Privacy or Compliance concerns?"}
      AwsPriv000 -->|Yes| AwsPriv600
      AwsPriv000 ---->|No| AwsML801
      AwsPriv600{"Does this project utilize a separate account for payment processing?"}
      AwsPriv600 --> AwsPriv604


      %% Machine Learning
      AwsML000{"Will this project be using machine learning before your next readiness review?"}
      AwsML000 -->|Yes| AwsML801
      AwsML801{"Do you have documented training data?"}
      AwsML801 --> AwsML802
      AwsML802{"Which interactive notebooks are you using?"}
      AwsML802 --> AwsML803
      AwsML803{"What is the code coverage for the data generation code?"}
      AwsML803 --> AwsML804
      AwsML804{"Do you automatically retrain each model?"}
      AwsML804 --> AwsML805
      AwsML805{"Do you automatically redeploy retrained models?"}
      AwsML805 --> AwsML806
      AwsML806{"What is your test coverage of model usage?"}
    end
```
