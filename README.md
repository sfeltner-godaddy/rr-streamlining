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
      AwsBase100 --> AwsBase103  %% Further review required
      AwsBase103{Which environments/accounts is this project expected to utilize?}
      AwsBase103 --> AwsBase108  %% Keep it!  Keep it base
      AwsBase108{Please describe all end users of this project:}
      AwsBase108 --> AwsBase109 %% Gate this with "Are there services im this account utilized by employees?""
      AwsBase109{"Is everything you are using in ADOPT on TechRadar?"}
      AwsBase109 --> AwsST01000  %% Maybe base/general

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
      AwsST01005 --> AwsData000  %% Gating questions on Service Tier 0/1

      %% AWS Data
      AwsData000{"Do you handle, process or store data in your service?"}
      AwsData000 -->|Yes| AwsData402
      AwsData000 ---->|No| AwsWeb000
      AwsData402{"For what purposes is data moved from Prod to Non-Prod environments?"}
      AwsData402 --> AwsData404   %% Keep it
      AwsData404{"Are all datastores compliant with all appropriate data retention policies?"}
      AwsData404 --> AwsData405   %% Ask Brittany
      AwsData405{"Is there a process in place to delete data that exceeds retention periods on at least a quarterly basis?"}
      AwsData405 --> AwsData406   %% Ask Brittany
      AwsData406{"What is your authentication model for accessing your database?"}
      AwsData406 --> AwsData407   %% Keep it
      AwsData407{Does your application store, process, and/or transmit P* data?}
      AwsData407 -->|Yes| AwsData408
      AwsData407 ---->|No| AwsWeb000
      AwsData408{"Sensitive or P*I Data must be application layer encrypted, please choose which method you are using to do so"}
      AwsData408 --> AwsData409  %% Keep it
      AwsData409{"Is there a process to securely delete PII data upon request?"}
      AwsData409 --> AwsWeb000   %% Keep it



      %% AWS Web Application
      AwsWeb000{"Does your service expose any UI or endpoints?"}  %% Reword
      AwsWeb000 -->|Yes| AwsWeb100
      AwsWeb000 ---->|No| AwsAppDev000
      AwsWeb100{How many requests per second will the most active endpoint receive?}
      AwsWeb100 --> AwsWeb101  %% DELETE all scaling related questions and defer to artifacts
      AwsWeb101{"Which of the following are used to protect any interface exposed outside of your AWS Accounts?"}
      AwsWeb101 --> AwsWeb102  %% Keep it
      AwsWeb102{"Select all domains this application will run on:"}
      AwsWeb102 --> AwsWeb103  %% Keep it
      AwsWeb103{"Web applications are utilizing the following CDNs for static assets: (check all that apply)"}
      AwsWeb103 --> AwsAppDev000  %% Keep for now - further review.  Maybe move to on-prem and acq


      %% AWS Applicaton Development
      AwsAppDev000{"YET ANOTHER GATING QUESTION - Do you have any App Dev concers?"}
      AwsAppDev000 -->|Yes| AwsAppDev201
      AwsAppDev000 ---->|No| AwsArch000
      AwsAppDev201{"Select all authentication systems the project is using:"}
      AwsAppDev201 --> AwsAppDev209  %% Keep, but gate
      AwsAppDev209{"Do all tools hosted in this account adhere to the Tool Security Standard in full?"}
      AwsAppDev209 --> AwsArch000  %% Keep but gate

      %% AWS Architecture
      AwsArch000{"NEED GATING QUESTION - Do you have any Architecture concerns?"}
      AwsArch000 -->|Yes| AwsArch300
      AwsArch000 ---->|No| AwsOps000
      AwsArch300{"Which methods would be used in this project to double/half capacity?"}
      AwsArch300 --> AwsArch301
      AwsArch301{"What are the traits that make up your service?"}
      AwsArch301 --> AwsOps000

      %% Operations
      AwsOps000{"NEED GATING QUESTION - Do you have any Operations concerns?"}
      AwsOps000 -->|Yes| AwsOps500
      AwsOps000 ---->|No| AwsPriv000
      AwsOps500{"Are all logs, monitors, and alerts configured in compliance with 'GoDaddy Monitoring Standard', and confirmed to be operating appropriately?"}
      AwsOps500 --> AwsOps501
      AwsOps501{"Is your application integrated with the SPAQ/Rigor platform to capture application metrics?"}
      AwsOps501 --> AwsOps502
      AwsOps502{"Are you adhering to the Real User Monitoring standard?"}
      AwsOps502 --> AwsOps503
      AwsOps503{"Have you identified recovery processes for each layer of your application?"}
      AwsOps503 --> AwsOps504
      AwsOps504{"Which parts of provisioning your infrastructure require manual steps and/or human intervention?"}
      AwsOps504 --> AwsOps505
      AwsOps505{"Do all deployments in this project generate change orders when deploying to production?"}
      AwsOps505 --> AwsOps506
      AwsOps506{"Do all production changes follow the Godaddy Change Management Policy?"}
      AwsOps506 --> AwsPriv000

      %% Privacy and Compliance
      AwsPriv000{"NEED GATING QUESTION - Do you have Privacy or Compliance concerns?"}
      AwsPriv000 -->|Yes| AwsPriv600
      AwsPriv000 ---->|No| AwsSec000
      AwsPriv600{"Does this project utilize a separate account for payment processing?"}
      AwsPriv600 --> AwsPriv604
      AwsPriv604{"Which of the following strategies do you apply for least privilege and zero trust?"}
      AwsPriv604 --> AwsPriv605
      AwsPriv605{"Is the system configured to issue a log entry when an account is added to or removed from any group assigned admin privileges?"}
      AwsPriv605 --> AwsPriv606
      AwsPriv606{"Will there be any admin access to any production resource beyond Break-Glass Procedure?"}
      AwsPriv606 --> AwsPriv607
      AwsPriv607{"Reusable deployment artifacts are stored in:"}
      AwsPriv607 --> AwsPriv608
      AwsPriv608{"Select all CI/CD methods utilized:"}
      AwsPriv608 --> AwsPriv609
      AwsPriv609{"Which source code management systems are used?"}
      AwsPriv609 --> AwsPriv610
      AwsPriv610{"How often do you upgrade your software/packages/libs?"}
      AwsPriv610 --> AwsPriv611
      AwsPriv611{"What controls are in place to limit administrative access to the systems?"}
      AwsPriv611 --> AwsPriv612
      AwsPriv612{"Do your CICD pipeline(s) utilized in this project require passing build, automated, and security tests including passing any security scans with no High/Critical vulnerabilities prior to deployment?"}
      AwsPriv612 --> AwsPriv613
      AwsPriv613{"Are there third-party or self-managed applications (libraries/dependencies) that will require patch management?"}
      AwsPriv613 --> AwsSec000

      %% Security
      AwsSec000{"I NEED GATING QUESTION - Do you have any Security Concerns?"}
      AwsSec000 -->|Yes| AwsSec700
      AwsSec000 ---->|No| AwsML000
      AwsSec700{"Is security logging applied to all systems and will it include application security logging for your production services prior to taking production traffic?"}
      AwsSec700 --> AwsSec701
      AwsSec701{"How are you monitoring for unauthorized transfer of sensitive and/or p*i information across the network? (you should evaluate your application log metadata for indications of threat actor abuse of your application)"}
      AwsSec701 --> AwsSec704
      AwsSec704{"What is your rotation strategy for all compute resources?"}
      AwsSec704 --> AwsSec706
      AwsSec706{"Will all unnecessary scripts, drivers, subsystems, library, dependencies, etc. be removed from systems in this project?"}
      AwsSec706 --> AwsSec707
      AwsSec707{"Are you compliant with the Service Authentication Patterns Standard?"}
      AwsSec707 --> AwsML000

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
