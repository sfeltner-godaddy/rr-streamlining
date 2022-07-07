# rr-streamlining

``` mermaid
%%{init: { "flowchart": { "htmlLabels": true, "curve": "linear", "logLevel": 1 } } }%%
graph TD
    AWS{Is this project AWS based?}
    OnPrem{Is this project on-prem?}
    Acquisition{Is this project from an acquisition?}
    End{end}

    AWS --->|Yes| AwsBase000
    AWS ---->|No| OnPrem
    OnPrem --->|Yes| OpBase000
    OnPrem -->|No| Acquisition
    Acquisition --->|Yes| AcqBase000
    Acquisition -->|No| End
    AcqOps102 ----> End
    AwsML000 ---->|No| End
    AwsML806 --> End
    OpML000 ---->|No| End
    OpML113 --> End

    %% AWS
    subgraph AWSG [AWSG]
      %% AWS Base Questions - No gating question.
      AwsBase000{Does your application adhere to all must haves in the Must Haves Should Dos?}
      AwsBase000 --> AwsBase101  %% Further review required
      AwsBase101{Which environments/accounts is this project expected to utilize?}
      AwsBase101 --> AwsBase102  %% Keep it!  Keep it base
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
      AwsBase109{"Is your application integrated with SPAQ to capture application metrics?"}
      AwsBase109 --> AwsBase110
      AwsBase110{"Have you identified recovery processes for each layer of your application?"}
      AwsBase110 --> AwsBase111  %% Keep
      AwsBase111{"Do all deployments in this project generate change orders when deploying to production?"}
      AwsBase111 --> AwsBase112  %% Keep
      AwsBase112{"Select all authentication systems the project is using:"}
      AwsBase112 --> AwsBase201  %% Keep, but gate - base

      AwsBase201{"Will employees access this service as an internal tool?"}
      AwsBase201 -->|Yes| AwsBase202
      AwsBase201 -->|No| AwsST01000
      AwsBase202{"Please describe all end users of this project:"}
      AwsBase202 --> AwsBase203 %% Gate this with "Are there services im this account utilized by employees?""
      AwsBase203{"Do all tools hosted in this account adhere to the Tool Security Standard in full?"}
      AwsBase203 --> AwsST01000  %% Keep but gate - base


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


    %% On-Prem Review questions
    subgraph OnpremG [OnPremG]
      %% On-prem Base Questions - No gating question.
      OpBase000{"Does your application adhere to all must haves in the Must Haves Should Dos?"}
      OpBase000 --> OpBase101
      OpBase101{"Do you have a plan to migrate to AWS within the next 12 months?"}
      OpBase101 ---> OpBase102
      OpBase102{"Does your application adhere to all must haves in the Must Haves Should Dos?"}
      OpBase102 ---> OpBase103
      OpBase103{"Which datacenters or colocations will this project utilize?"}
      OpBase103 ---> OpBase104
      OpBase104{"Please describe all end users of this project:"}
      OpBase104 ---> OpBase105
      OpBase105{"Have all components been constructed in compliance with GoDaddy Software Development Policy?"}
      OpBase105 ---> OpBase106
      OpBase106{"Is everything you are using in ADOPT on TechRadar?"}
      OpBase106 ---> OpBase107
      OpBase107{"Is your application integrated with the SPAQ/Rigor platform to capture application metrics?"}
      OpBase107 ---> OpBase108
      OpBase108{"Have you identified recovery processes for each layer of your application?"}
      OpBase108 ---> OpBase109
      OpBase109{"Do all deployments in this project generate change orders when deploying to production?"}
      OpBase109 ---> OpBase110
      OpBase110{"Is all user access to servers managed by AD?"}
      OpBase110 ---> OpBase111
      OpBase111{"Reusable deployment artifacts are stored in:"}
      OpBase111 ---> OpBase112
      OpBase112{"Is all source code managed through GitHub Enterprise Cloud?"}
      OpBase112 ---> OpBase113
      OpBase113{"How often do you upgrade your software/packages/libs?"}
      OpBase113 ---> OpBase114
      OpBase114{"Is security logging applied to all systems and will it include application security logging?"}
      OpBase114 ---> OpBase115
      OpBase115{"Select all authentication systems the project is using:"}
      OpBase115 ---> OpBase201

      OpBase201{"Will employees access this service as an internal tool?"}
      OpBase201 -->|Yes| OpBase202
      OpBase201 -->|No| OpST01000
      OpBase202{"Please describe all end users of this project:"}
      OpBase202 --> OpBase203 %% Gate this with "Are there services im this account utilized by employees?""
      OpBase203{"Do all tools hosted in this account adhere to the Tool Security Standard in full?"}
      OpBase203 --> OpST01000  %% Keep but gate - base

      OpST01000{"Is your service a Service Tier 0 or 1?"}
      OpST01000 -->|Yes| OpST01101
      OpST01000 ---->|No| OpWeb000
      OpST01101{"Do your CICD pipeline(s) utilized in this project require passing build, automated, and security tests including passing any security scans with no High/Critical vulnerabilities prior to deployment?"}
      OpST01101 --> OpData000

      OpData000{"Do you process or store data in your service?"}
      OpData000 -->|Yes| OpData101
      OpData000 ---->|No| OpWeb000
      OpData101{"For what purposes is data moved from Prod to Non-Prod environments?"}
      OpData101 --> OpData102
      OpData102{"Are all datastores compliant with all appropriate data retention policies?"}
      OpData102 --> OpData103
      OpData103{"Is there a process in place to delete data that exceeds retention periods on at least a quarterly basis?"}  %% Is this redundant?
      OpData103 --> OpData104
      OpData104{"What is your authentication model for accessing your database?"}
      OpData104 --> OpData105
      OpData105{"Does your application store, process, and/or transmit P data?"}
      OpData105 --> OpData106
      OpData106{"Is there a process to securely delete PII data upon request?"}
      OpData106 --> OpWeb000

      OpWeb000{"Does your service expose any UI or endpoints outside of your AWS accounts?"}  %% Reword
      OpWeb000 -->|Yes| OpWeb101
      OpWeb000 ---->|No| OpML000
      OpWeb101{"Select all domains this application will run on:"}
      OpWeb101 --> OpML000

      OpML000{"Will this project be using machine learning before your next readiness review?"}
      OpML000 -->|Yes| OpML101
      OpML101{"Which of the following are used to protect any interface exposed outside of your AWS Accounts?"}
      OpML101 --> OpML102
      OpML102{"What is your rotation strategy for all compute resources?"}
      OpML102 --> OpML103
      OpML103{"Sensitive or P*I Data must be application layer encrypted, please choose which method you are using to do so"}
      OpML103 --> OpML104
      OpML104{"Will all unnecessary scripts, drivers, subsystems, library, dependencies, etc. be removed from systems in this project?"}
      OpML104 --> OpML105
      OpML105{"Are you compliant with the Service Authentication Patterns Standard?"}
      OpML105 --> OpML106
      OpML106{"Will this project be using machine learning before your next readiness review?"}
      OpML106 --> OpML107
      OpML107{"Do you have documented training data?"}
      OpML107 --> OpML108
      OpML108{"Which interactive notebooks are you using?"}
      OpML108 --> OpML109
      OpML109{"What is the code coverage for the data generation code?"}
      OpML109 --> OpML110
      OpML110{"Do you automatically retrain each model?"}
      OpML110 --> OpML111
      OpML111{"Do you automatically redeploy retrained models?"}
      OpML111 --> OpML112
      OpML112{"What is your test coverage of model usage?"}
      OpML112 --> OpML113
      OpML113{"What changes could we make to this readiness review process to improve it?"}
    end

    %% Acquisition Based Questions
    subgraph AcquisitionG [AcquisitionG]
      AcqBase000{"We have acquisition questions for you!"}
      AcqBase000 ---> AcqData101
      AcqData101{"We have acquisition data questions for you!"}
      AcqData101 ---> AcqOps102
      AcqOps102{"We have acquisition Ops questions for you!"}

      %% Privacy and Compliance
      AwsPriv000{"NEED GATING QUESTION - Do you have Privacy or Compliance concerns?"}
      AwsPriv000 -->|Yes| AwsPriv600
      AwsPriv000 ---->|No| AwsML801
      AwsPriv600{"Does this project utilize a separate account for payment processing?"}
      AwsPriv600 --> AwsPriv604
    end
```
