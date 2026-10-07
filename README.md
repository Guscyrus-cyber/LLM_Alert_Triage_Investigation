AI-Assisted SOC Lab — LLM Alert Triage, Investigation & Documentation

Introduction

This lab demonstrates how a Large Language Model (LLM) can assist a Tier-1 SOC analyst throughout a security investigation. A simulated authentication incident is used across nine investigation steps, with each step demonstrating a different AI-assisted SOC skill.

The investigation covers alert triage, evidence correlation, investigation planning, KQL/SPL query generation, MITRE ATT&CK mapping, AI hallucination detection, alert classification, incident documentation, and Tier-1 to Tier-2 escalation.

SOC Analyst and LLM Roles

Throughout the lab, the SOC analyst creates and provides the investigation context. The investigation context is derived from evidence already collected and validated during the investigation, including security alerts, authentication logs, SIEM events, EDR telemetry, and findings established during earlier investigation stages.

The SOC analyst also creates the LLM prompt. The prompt defines the specific assistance required from the LLM, such as analyzing authentication behavior, correlating security events, developing an investigation plan, generating hunting queries, mapping behavior to MITRE ATT&CK, evaluating conclusions, classifying an alert, or producing incident documentation.

The Scenario / Evidence and LLM Prompt are then submitted together to the LLM.

The LLM analyzes only the supplied information and produces the requested output. Depending on the investigation stage, the LLM may summarize security activity, correlate indicators, generate queries, identify possible ATT&CK techniques, recommend additional evidence for examination, or assist with SOC documentation.

The resulting LLM output is then reviewed by the SOC analyst, who validates the findings against the original security evidence and identifies unsupported assumptions, incorrect conclusions, or hallucinated information.

The operational workflow used throughout the lab is:

Scenario / Evidence → LLM Prompt → LLM Submission → LLM Output → SOC Analyst Validation

The LLM serves as an investigative assistant rather than the final decision-maker. Security conclusions remain dependent on validated telemetry and analyst review.

Lab Structure

The lab consists of nine LLM-assisted SOC skills:

1.  LLM-Assisted Initial Alert Triage

2.  LLM-Assisted Evidence Extraction and Correlation

3.  LLM-Assisted Investigation Planning

4.  LLM-Assisted KQL/SPL Query Generation

5.  LLM-Assisted MITRE ATT&CK Mapping

6.  LLM-Assisted Detection of Unsupported Conclusions and Hallucinations

7.  LLM-Assisted Alert Classification

8.  LLM-Assisted Incident Documentation

9.  LLM-Assisted Tier-1 to Tier-2 Escalation/Handoff

Each step uses the same developing authentication incident while introducing a distinct SOC skill and a different use of the LLM.

LLM Used: ChatGPT

ChatGPT was used as the Large Language Model (LLM) for this lab. The SOC analyst supplied validated investigation context and structured prompts to ChatGPT for AI-assisted analysis. ChatGPT generated investigative assistance such as event analysis, evidence correlation, investigation planning, query generation, MITRE ATT&amp;CK mapping, alert classification, and incident documentation. All LLM-generated output was reviewed and validated by the SOC analyst before being accepted as part of the investigation.

In this skills in real scenario, Authentication Events coming from the organization's actual security systems—such as Microsoft Entra ID sign-in logs, Windows Event Logs, Active Directory, VPN logs, EDR/XDR, Microsoft Sentinel, Splunk, or another SIEM. An alert in the SIEM might lead the SOC analyst to retrieve the relevant authentication events. LLM Prompt coming from the SOC analyst. After examining the alert and available evidence, the analyst decides what assistance is needed and writes instructions for the LLM. For example: analyze these authentication events, identify suspicious patterns, and recommend additional evidence to investigate.

Step 1 — LLM-Assisted Initial Alert Triage

Objective

For this lab, I use a Large Language Model (LLM) to analyze authentication telemetry, summarize the activity, identify important indicators, recognize suspicious patterns, and recommend additional investigation.

Scenario

A SIEM generated the following alert:

Alert: Multiple Failed Sign-ins Followed by Successful Authentication\
Severity: Medium\
Account: j.smith\
Source: Authentication logs

Based on Authentication Events and LLM Prompt I generated from my previous lab.\
Real Source: Authentication events were obtained from labs such as Microsoft Entra ID Sign-in Logs ingested into Microsoft Sentinel for SOC investigation. And I summited them to LLM (Large Language Model) Which I used ChatGPT for this lab.

LLM Analysis

The LLM identified eight failed authentication attempts against j.smith, followed by one successful authentication. All nine events originated from 198.51.100.74.

The sequence occurred between 20:41:03 and 20:43:12, representing approximately 2 minutes and 9 seconds of authentication activity.

The observed pattern was:

8 failed authentications → 1 successful authentication

Repeated password failures followed by successful authentication can be consistent with password guessing or brute-force behavior. The available evidence does not establish malicious activity because legitimate password-entry mistakes could produce a similar sequence.

Additional investigation should include authentication history, MFA results, device information, source-IP activity against other accounts, post-authentication activity, endpoint alerts, and relevant threat-intelligence information.

Analyst Validation

The LLM correctly summarized the authentication sequence and avoided presenting a possible brute-force attack as a confirmed compromise.

The source address 198.51.100.74 belongs to the reserved TEST-NET-2 (198.51.100.0/24) documentation range. The address represents simulated telemetry rather than a real external threat indicator.

Any LLM claim identifying the address as a known malicious attacker would therefore represent an unsupported or fabricated conclusion.

SOC Learning Point

LLM-generated analysis provides investigative assistance rather than authoritative security evidence.

AI-generated findings require validation against original logs, SIEM/EDR telemetry, identity data, threat intelligence, and other authoritative security sources.\
\
Authentication Events: I created simulated authentication events based on authentication patterns and security concepts practiced in my previous Microsoft Entra ID and SOC investigation labs.\
\
2026-09-17 20:41:03 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:41:17 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:41:31 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:41:44 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:42:01 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:42:19 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:42:36 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:42:54 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:43:12 \| j.smith \| 198.51.100.74 \| SUCCESS \| Authentication successful

LLM Prompt: I created a structured LLM prompt based on the investigation objective and the available authentication evidence. I submitted the authentication events and prompt to ChatGPT for LLM-assisted analysis.\
\
Act as an AI assistant supporting Tier-1 SOC alert triage.

Analyze the provided authentication events.

1\. Summarize the authentication activity.

2\. Identify important entities and indicators.

3\. Identify suspicious behavioral patterns.

4\. Recommend additional evidence for investigation.

5\. Do not classify the activity as malicious unless sufficient evidence exists.

6\. Clearly separate observed facts from assumptions.\
\
So, I prepared these two primary inputs for this exercise: simulated authentication telemetry based on previous authentication labs and a structured LLM prompt for Tier-1 SOC alert triage.

Step 2 — LLM-Assisted Evidence Extraction and Correlation

Objective

I use an LLM to extract important security evidence from multiple authentication events and correlate activity across accounts, source IP addresses, timestamps, and authentication results.

Additional Authentication Evidence

The investigation produced additional authentication events:

2026-09-17 20:40:51 \| a.lee \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:41:03 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:41:17 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:41:31 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:41:44 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:42:01 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:42:19 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:42:36 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:42:54 \| j.smith \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:43:12 \| j.smith \| 198.51.100.74 \| SUCCESS \| Authentication successful

2026-09-17 20:43:29 \| m.garcia \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:43:46 \| r.patel \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:44:02 \| a.lee \| 198.51.100.74 \| FAILED \| Invalid password

2026-09-17 20:44:31 \| j.smith \| 203.0.113.25 \| SUCCESS \| MFA successful

LLM Prompt

Act as an AI assistant supporting a Tier-1 SOC investigation.
Analyze and correlate the provided authentication events.
1. Extract all user accounts and source IP addresses.
2. Count failed and successful authentications for each account.
3. Identify accounts targeted by the same source IP.
4. Identify authentication events occurring close together in time.
5. Identify behavioral patterns that warrant further investigation.
6. Compare the evidence with the earlier pattern of repeated failures followed by success.\
7. Clearly separate observed evidence from possible interpretations.
8. Do not invent geolocation, reputation, ownership, device, or threat-intelligence information that is not present in the logs.
9. Do not make a final malicious/benign classification.

I submitted both to LLM (ChatGPT).

LLM Correlation Analysis
-----------------------------------

The supplied authentication telemetry contains four user accounts and two source IP addresses.

| Account  | Failed | Successful | Source IP(s)                |
|----------|--------|------------|-----------------------------|
| j.smith  | 8      | 2          | 198.51.100.74, 203.0.113.25 |
| a.lee    | 2      | 0          | 198.51.100.74               |
| m.garcia | 1      | 0          | 198.51.100.74               |
| r.patel  | 1      | 0          | 198.51.100.74               |

Evidence Correlation

Source IP 198.51.100.74 generated failed authentication attempts against four different accounts: (Image 1)

A second source IP, 203.0.113.25, later produced a successful MFA authentication for j.smith\

Observed Evidence

The following findings are directly supported by the telemetry:

198.51.100.74 interacted with four accounts.

Twelve failed authentications originated from 198.51.100.74.

Eight failures against j.smith were followed by successful authentication from the same source.

Failed authentication attempts against other accounts occurred before and after the j.smith activity.

j.smith subsequently completed successful MFA authentication from 203.0.113.25.

The entire displayed event sequence occurred within approximately four minutes.

Possible Interpretations

The activity from 198.51.100.74 could resemble password-spraying or credential-guessing behavior because one source address attempted authentication against several accounts.

However, the available telemetry does not establish:

IP reputation, geographic location, attacker identity, device identity, account compromise, credential theft, or malicious intent.

The later successful MFA event also does not prove that the earlier successful authentication was malicious or legitimate.
\
Analyst Validation

Manual comparison against the raw telemetry confirms the LLM's principal correlation:

One source IP → multiple accounts → repeated authentication failures → successful authentication against j.smith.

The correlation makes the activity more significant than the isolated j.smith sequence examined during Step 1, but additional evidence remains necessary before final classification.

A further lab-specific validation is important: both 198.51.100.74 and 203.0.113.25 belong to documentation address ranges, so no real-world threat reputation should be attributed to either address.

Step 1 demonstrated LLM-assisted summarization.

Step 2 demonstrates LLM-assisted correlation:

Individual events → shared indicators → relationships between accounts → behavioral pattern → investigation lead

The LLM accelerated evidence organization, while the underlying authentication telemetry remained the authoritative evidence source.

Step 3 — LLM-Assisted Investigation Planning

Objective

I use an LLM to create a prioritized SOC investigation plan based on the evidence identified during Steps 1 and 2.

The goal is not to ask the LLM for a verdict. The goal is to determine which evidence should be examined next and why.

Current Investigation Context

The following findings were established during the previous steps:

Account: j.smith

Source IP: 198.51.100.74

\- 8 failed authentications against j.smith

\- 1 successful authentication against j.smith

\- Failed authentications against a.lee

\- Failed authentication against m.garcia

\- Failed authentication against r.patel

Second source IP: 203.0.113.25

\- Successful MFA authentication for j.smith

Current status:

Suspicious authentication behavior requiring further investigation.

No confirmed account compromise.

LLM Prompt

Act as an AI assistant supporting a Tier-1 SOC investigation.

Create a prioritized investigation plan for the authentication activity.

For each recommended investigation step:

1\. Identify the evidence or telemetry that should be examined.

2\. Explain why that evidence is important.

3\. Explain what finding would increase suspicion.

4\. Explain what finding would reduce suspicion.

5\. Place the investigation steps in a logical SOC investigation order.

Consider evidence such as:

\- Authentication history

\- MFA records

\- Source-IP activity

\- Other targeted accounts

\- Device information

\- User-agent information

\- Endpoint/EDR telemetry

\- Post-authentication activity

\- Password or account changes

\- Threat-intelligence information

Do not assume information that is not present in the evidence.

Do not invent IP reputation, geolocation, device information, or threat-intelligence results.

Do not make a final malicious or benign classification.
\
I Submit the investigation context together with the LLM Prompt.\
\
Analyst Validation

After generation of the investigation plan, validation should focus on three questions:

Is every recommended investigation relevant? Is the proposed order reasonable? Did the LLM invent evidence that does not exist?

For example:

198.51.100.74 is a known malicious IP.

would be an invalid statement because no threat-intelligence result was provided.

In contrast:\
\
Check available threat-intelligence sources for information associated with 198.51.100.74.

would represent an appropriate investigation recommendation, rather than an unsupported factual claim.\
\
SOC Learning Point

The LLM is being used as an investigation-planning assistant, not as the decision maker.\
\
(Images 2 and 3)

Prioritized Investigation Plan

LLM Correlation Assessment

The highest-priority investigation should focus on identity evidence because the original alert concerns authentication.

The most significant existing correlation remains:\
\
198.51.100.74

\|

+--\> a.lee FAILED

+--\> j.smith FAILED × 8

+--\> j.smith SUCCESS

+--\> m.garcia FAILED

+--\> r.patel FAILED\
\
This pattern warrants examination for possible credential-guessing or password-spraying behavior, but the available evidence remains insufficient for a final classification.

The successful MFA authentication from 203.0.113.25 should also be correlated with authentication history, device information, session information, and MFA records. A successful MFA event alone does not establish whether the earlier authentication from 198.51.100.74 was legitimate or unauthorized.

Observed Evidence vs. Investigation Hypotheses

Observed evidence: Multiple accounts received failed authentication attempts from the same source address. j.smithexperienced eight failures followed by a successful authentication. A later successful MFA authentication for j.smithoriginated from a second address.

Investigation hypotheses: Password spraying, brute-force activity, credential compromise, legitimate password mistakes, expected authentication infrastructure, and normal user activity remain possibilities requiring additional evidence.

No IP reputation, geographic location, device identity, malware activity, or account compromise can be established from the supplied telemetry.

Analyst Validation

The LLM-generated plan follows a reasonable investigation sequence:

Identity evidence → MFA → source/account correlation → device/session → endpoint → post-authentication activity → account changes → threat intelligence

No unsupported threat-intelligence, geolocation, device, or attacker information was introduced.

SOC Learning Point

Step 3 demonstrates that an LLM can help transform a suspicious alert into a structured investigation plan while maintaining separation between:

Known evidence → investigation hypothesis → evidence required for confirmation

The final security determination remains dependent on validated telemetry rather than LLM-generated conclusions.

Step 4 — LLM-Assisted KQL/SPL Query Generation

Objective

I use an LLM to translate a natural-language SOC investigation question into KQL and SPL hunting queries.

The generated queries support investigation of authentication failures originating from the same source IP and targeting multiple accounts.

Investigation Question

The authentication evidence from Steps 1–3 established repeated failed authentication attempts from 198.51.100.74 against several accounts.

The investigation question is:

Which source IP addresses generated repeated failed authentication attempts against multiple user accounts within a short period?

LLM Prompt\
\
Act as an AI assistant supporting a SOC threat-hunting investigation.

Generate two hunting queries for detecting repeated failed

authentication attempts from the same source IP against

multiple user accounts.

Query 1: Microsoft Sentinel KQL

Assume the SigninLogs table contains:

TimeGenerated

UserPrincipalName

IPAddress

ResultType

Query 2: Splunk SPL

Assume authentication events contain:

\_time

user

src_ip

action

Requirements:

1\. Search failed authentication events.

2\. Group activity by source IP.

3\. Count total failed authentication attempts.

4\. Count distinct targeted user accounts.

5\. Return activity involving at least 5 failed attempts

against at least 3 different accounts.

6\. Include the first and last observed timestamps.

7\. Sort the most suspicious activity first.

8\. Explain the purpose of each query.

9. Do not invent fields outside the supplied schemas.
\
I submitted the above prompt to LLM.\
\
LLM Output:

The LLM generated two queries resembling the following structure. (Images 4 and 5)

KQL:\
\

SPL:

Analyst Validation

LLM-generated queries require validation before production use.

Validation should confirm:

Correct data source → correct field names → correct failure condition → correct aggregation → correct thresholds → correct time handling

The KQL example deserves particular attention. ResultType != "0" can serve as a broad failure filter for the simulated exercise, but a real Sentinel investigation should validate the relevant result/error codes and data semantics before treating every nonzero result as the desired category of failed authentication.

The SPL example similarly assumes action="failure" because the simulated schema explicitly defines the action field. Production Splunk environments may use different field names or values.

SOC Learning Point

Natural-language investigation questions can be converted into hunting queries with LLM assistance:

Investigation question → LLM-generated KQL/SPL → analyst reviews syntax and logic → query testing → investigation results

An LLM can accelerate query development, but generated queries should never be assumed correct solely because the syntax appears valid.

## LLM-Generated Hunting Queries

Microsoft Sentinel — KQL

Purpose: The query searches unsuccessful authentication events, groups events by source IP address, counts failed attempts and distinct targeted accounts, records the first and last observed timestamps, and returns source addresses associated with at least five failures against at least three accounts. (Images 6 and 7)

Splunk — SPL

Purpose: The query searches failed authentication events, groups activity by source IP address, counts authentication failures and distinct targeted accounts, records the first and last event timestamps, and prioritizes source addresses with the highest number of failed attempts.

LLM Output Review

Both queries satisfy the supplied investigation requirements and use only fields defined in the prompt. One validation consideration applies to the KQL query: ResultType != "0" treats every nonzero result as an unsuccessful authentication. Production Microsoft Entra ID data can contain different result codes representing different authentication outcomes. Production deployment therefore requires validation of the desired ResultType values.

The SPL query assumes that failed authentication events are represented by: action="failure"\
\
SOC Learning Point

The LLM converted a natural-language security question into two different SIEM query languages:

Natural-language investigation requirement → LLM → KQL/SPL → analyst validation

LLM-generated queries accelerate threat hunting but require verification of field names, data semantics, filters, thresholds, and query logic before operational use.

Step 5 — LLM-Assisted MITRE ATT&CK Mapping


Objective

I use an LLM to identify possible MITRE ATT&CK techniques associated with the observed authentication behavior.

No ATT&CK technique is assigned before LLM analysis and analyst validation.

Scenario / Evidence

The investigation has established the following evidence:\
\
Authentication Investigation Summary

Source IP: 198.51.100.74

Observed activity:

\- 8 failed authentications against j.smith

\- 1 successful authentication against j.smith

\- 2 failed authentications against a.lee

\- 1 failed authentication against m.garcia

\- 1 failed authentication against r.patel

Additional event:

\- j.smith later completed successful MFA authentication

from 203.0.113.25

Observed pattern:

\- One source IP attempted authentication against multiple accounts.

\- Repeated authentication failures occurred within a short period.

\- A successful authentication against j.smith followed repeated failures.

Current investigation status:

\- Suspicious authentication activity

\- No confirmed account compromise

\- No confirmed attacker identity

\- No confirmed credential theft\
\
LLM Prompt\
\
Act as an AI assistant supporting a Tier-1 SOC investigation.

Analyze the supplied authentication evidence and identify

potential MITRE ATT&CK Enterprise techniques or sub-techniques

relevant to the observed behavior.

Requirements:

1\. Provide the MITRE ATT&CK technique or sub-technique name.

2\. Provide the corresponding ATT&CK ID.

3\. Explain which observed evidence supports each mapping.

4\. Separate strongly supported mappings from possible mappings.

5\. Identify any mapping that cannot be established from the

available evidence.

6\. Do not assume credential theft, malware execution, lateral

movement, persistence, privilege escalation, or account

compromise without supporting evidence.

7\. Do not make a final malicious or benign classification.

8\. Limit the analysis to techniques directly relevant to the supplied authentication evidence.

I submitted both Scenario / Evidence and prompt to LLM.
\
Analyst Task

No ATT&CK answer is provided at this stage.

The LLM response becomes the evidence for the next portion of Step 5. ATT&CK IDs, technique names, and reasoning will then be independently validated before inclusion in the investigation findings.

SOC Learning Point

Step 5 tests whether an LLM can assist with:

Observed behavior → ATT&CK hypothesis → technique/ID → evidence justification → analyst validation

LLM-Assisted MITRE ATT&CK Mapping

LLM Analysis

The authentication evidence most directly maps to the Brute Force family within the MITRE ATT&CK Credential Access tactic. (Image 8)\

MITRE ATT&CK documents Brute Force as T1110 and separately identifies techniques involving valid accounts as T1078. 

Unsupported Mappings

The supplied evidence does not establish:

Credential dumping, MFA bypass, malware execution, persistence, privilege escalation, lateral movement, account manipulation, or credential theft.

No corresponding ATT&CK mappings should be assigned based solely on the available authentication events.

Analyst Validation

The strongest evidence supports Password Guessing (T1110.001).

Password Spraying (T1110.003) remains a hypothesis because multiple accounts were targeted from one source, but the telemetry does not reveal whether a common password was used across those accounts.

Valid Accounts (T1078) should not be treated as confirmed because the successful authentication does not establish unauthorized use.

Step 6 — LLM-Assisted Detection of Unsupported Conclusions and Hallucinations

Objective

I use an LLM to review an AI-generated SOC analysis and identify statements that are supported, unsupported, or require additional evidence.

### Scenario / Evidence\
Validated Authentication Evidence



- 198.51.100.74 generated failed authentication attempts

against four user accounts.

j.smith experienced 8 failed authentications followed

by 1 successful authentication from 198.51.100.74.

- j.smith later completed successful MFA authentication

from 203.0.113.25.

- No device information is available.

- No geolocation information is available.

- No IP reputation results are available.

- No endpoint/EDR evidence is available.

- No post-authentication activity has been examined.

- No confirmed account compromise exists.
\
AI-Generated SOC Analysis for Review\
The authentication activity represents a confirmed brute-force\
attack originating from a malicious IP address outside the United States.\
The attacker successfully compromised the j.smith account after eight password attempts.\
The successful login indicates that the attacker obtained the correct password.\
The attacker subsequently bypassed MFA and established access to the corporate environment.\
The failed authentication attempts against a.lee, m.garcia, and r.patel may indicate password-spraying behavior.\
Additional authentication and endpoint investigation is\
recommended before determining the full scope of the activity.

LLM Prompt\
\
Act as an AI assistant supporting SOC quality assurance.

Compare the AI-generated SOC analysis with the validated authentication evidence.

For every significant claim in the AI-generated analysis:

1. Classify the claim as:

- Supported by evidence

- Possible but not established

- Unsupported / hallucinated

2. Identify the specific evidence supporting or contradicting
the claim.

3. Identify additional evidence required to validate claims

that cannot currently be established.

4. Flag any statement that presents an assumption as a fact.

5. Do not introduce new facts that are absent from the

validated evidence.

6. Produce a corrected SOC analysis containing only conclusions

 justified by the available evidence.

I Submitted the Scenario / Evidence, AI-Generated SOC Analysis for Review, and LLM Prompt to the LLM.

LLM Quality-Assurance Analysis

Claim Evaluation

Additional Evidence Required

Confirmation of the unsupported or uncertain claims would require evidence such as authentication details, MFA records, IP reputation and geolocation data, device/session information, EDR telemetry, post-authentication activity, and account history.

Assumptions Presented as Facts

The original AI analysis incorrectly converted several hypotheses into factual statements:
\
"confirmed brute-force attack"

"malicious IP address"

"outside the United States"

"attacker successfully compromised"

"attacker obtained the correct password"

"attacker subsequently bypassed MFA"

"established access to the corporate environment"

None of those conclusions can be established from the supplied evidence


Repeated failed authentication attempts were observed from 198.51.100.74 against four user accounts. (Images 9 and 10)



. The j.smith account experienced eight failed authentication

attempts followed by one successful authentication from the
same source IP.

. The pattern warrants investigation for possible credential-

guessing activity. Authentication attempts involving multiple

accounts may also warrant investigation for possible

password-spraying behavior.

. A later successful MFA authentication for j.smith originated

from 203.0.113.25.

. The available evidence does not establish malicious IP

reputation, geographic origin, account compromise, credential

theft, MFA bypass, attacker identity, or post-authentication
access.

. Additional authentication, identity, session, and endpoint

evidence is required before final classification.
\
Analyst Validation

The LLM successfully distinguished observed evidence from unsupported AI assertions. The original AI analysis demonstrated a major generative-AI risk in security operations: plausible language can make an unsupported conclusion appear authoritative.

Step 7 — LLM-Assisted Alert Classification

Objective

I use an LLM to evaluate accumulated investigation evidence and recommend an alert classification while clearly identifying uncertainty and missing evidence.

Scenario / Evidence:
\
Authentication Investigation Evidence

Account: j.smith

### Authentication activity:

### - 8 failed authentications against j.smith from 198.51.100.74.

### - 1 successful authentication against j.smith from 198.51.100.74.

### - 2 failed authentications against a.lee from 198.51.100.74.

### - 1 failed authentication against m.garcia from 198.51.100.74.

### - 1 failed authentication against r.patel from 198.51.100.74.

### - j.smith later completed successful MFA authentication from 203.0.113.25.

### Correlation findings:

### - One source IP generated failed authentications against four accounts.

### - Repeated failures against j.smith were followed by successful authentication.

### - Activity occurred within a short time period.

### MITRE ATT&CK investigation:

### - Authentication behavior is consistent with possible credential-guessing activity.

### - Activity across multiple accounts may be consistent with password spraying.

### - Account compromise has not been established.

### Evidence limitations:

### - No device information is available.

### - No IP reputation information is available.

### - No geolocation information is available.

### - No endpoint/EDR telemetry is available.

### - No post-authentication activity has been examined.

### - No confirmed credential theft exists.

### - No confirmed account compromise exists.\
\
LLM Prompt:\
\
Act as an AI assistant supporting Tier-1 SOC alert classification.

### Evaluate the supplied authentication investigation evidence.

### 1. Recommend one of the following classifications:

###  - True Positive

###  - False Positive

###  - Benign Positive

###  - Suspicious / Requires Further Investigation

### 2. Explain which evidence supports the recommended classification.

### 3. Identify evidence that prevents a higher-confidence classification.

### 4. Explain what additional evidence could change the classification.

### 5. Assign a confidence level:

###  - Low

###  - Medium

###  - High

### 6. Clearly separate observed facts from interpretations.

### 

### 7. Do not assume attacker identity, credential theft, account

###  compromise, malicious IP reputation, geolocation, MFA bypass,

###  or endpoint compromise without supporting evidence.

8. Do not invent missing telemetry.\
\
I Submitted the Scenario / Evidence and LLM Prompt to the LLM.\
\
LLM Alert Classification Output


### Recommended Classification

Suspicious / Requires Further Investigation

Confidence Level: Medium

### Evidence Supporting the Classification

The following facts are directly supported by the supplied evidence:

198.51.100.74 generated failed authentication attempts against four accounts.

j.smith experienced eight failed authentications followed by one successful authentication from the same source IP.

Failed authentication activity against multiple accounts occurred within a short period.

j.smith later completed successful MFA authentication from 203.0.113.25.

No confirmed account compromise has been established.

### The combination of repeated authentication failures, multiple targeted accounts, and a subsequent successful authentication warrants continued investigation.\
\
Evidence Preventing Higher-Confidence Classification

A True Positive classification cannot currently be established because important evidence remains unavailable:

Device information\
IP reputation\
Geolocation\
Endpoint/EDR telemetry\
Post-authentication activity\
Confirmation of credential theft\
Confirmation that the successful authentication was unauthorized

### A False Positive or Benign Positive classification also cannot currently be established because no evidence explains the authentication pattern as expected or legitimate activity.\
\
Evidence That Could Change the Classification

Evidence supporting unauthorized access—such as suspicious post-login activity, an unrecognized device, correlated endpoint detections, or confirmation that the legitimate account holder did not perform the authentication—would strengthen a malicious interpretation.

Evidence demonstrating expected authentication behavior, recognized infrastructure, a known device/session, or confirmed legitimate account activity could support a benign interpretation.

### Observed Facts vs. Interpretation

Observed facts: Multiple accounts received failed authentication attempts from the same source IP. j.smith experienced repeated failures followed by successful authentication.

### Interpretation: The pattern is consistent with possible credential-guessing or password-spraying activity, but the available evidence does not establish malicious activity or account compromise.\
\
Analyst Validation

The LLM classification is consistent with the supplied evidence. Suspicious / Requires Further Investigation appropriately preserves uncertainty rather than converting suspicious authentication behavior into a confirmed security incident.

No unsupported attacker identity, credential theft, IP reputation, geolocation, MFA bypass, or endpoint-compromise claims were introduced.

Step 8 — LLM-Assisted Incident Documentation

### Objective

Use an LLM to transform validated investigation findings into concise, professional SOC incident documentationsuitable for an incident ticket or case record.

### Scenario / Evidence:\
\
Incident: Suspicious Authentication Activity

### Account:

### j.smith

### Authentication evidence:

### - 8 failed authentications against j.smith from 198.51.100.74.

### - 1 successful authentication against j.smith from 198.51.100.74.

### - 2 failed authentications against a.lee from 198.51.100.74.

### - 1 failed authentication against m.garcia from 198.51.100.74.

### - 1 failed authentication against r.patel from 198.51.100.74.

### - j.smith later completed successful MFA authentication from 203.0.113.25.

### Correlation findings:

### - 198.51.100.74 generated failed authentications against four accounts.

### - Repeated failures against j.smith were followed by successful authentication.

### - Authentication activity occurred within a short period.

### ATT&CK assessment:

### - Possible Password Guessing — T1110.001

### - Possible Password Spraying — T1110.003

### - Account compromise has not been established.

### Alert classification:

### Suspicious / Requires Further Investigation

### 

### Confidence:

### Medium

### Evidence limitations:

### - No device information available.

### - No IP reputation information available.

### - No geolocation information available.

### - No endpoint/EDR telemetry available.

### - No post-authentication activity examined.

### - No confirmed credential theft.

### - No confirmed account compromise.\
\
LLM Prompt:\
\
Act as an AI assistant supporting Tier-1 SOC incident documentation.

### Create professional incident documentation from the supplied

### validated investigation evidence.

### Include:

### 1. Incident title

### 2. Severity

### 3. Incident summary

### 4. Affected account(s)

### 5. Key indicators

### 6. Investigation findings

### 7. Relevant MITRE ATT&CK mappings

### 8. Current classification and confidence level

### 9. Evidence limitations

### 10. Recommended next investigation actions

### Requirements:

### - Use concise SOC ticket/case-note language.

### - Clearly distinguish confirmed observations from possible interpretations.

### - Do not claim confirmed malicious activity or account compromise.

### - Do not invent evidence.

### - Do not invent IP reputation, geolocation, device, endpoint,

###  credential-theft, or MFA-bypass information.

### - Preserve the supplied ATT&CK mappings as possible rather than confirmed.

- Base the documentation only on the supplied evidence.\
\
I submitted the Scenario / Evidence and LLM Prompt to the LLM.\
\
LLM-Generated Incident Documentation


### . Incident Title: Suspicious Authentication Activity — Multiple Failed Sign-ins Followed by Successful Authentication

### . Severity: Medium

### . Incident Summary: Multiple failed authentication attempts were observed from 198.51.100.74 against four user accounts. Account j.smithreceived eight failed authentication attempts followed by one successful authentication from the same source IP.

A later successful MFA authentication for j.smith originated from 203.0.113.25.

The observed activity warrants further investigation. Available evidence does not confirm malicious activity or account compromise.

### . Affected Accounts

j.smith\
a.lee\
m.garcia\
r.patel

### . Key Indicators

| Indicator | Observation |
|----|----|
| 198.51.100.74 | Failed authentication activity against four accounts; successful authentication against j.smith |
| 203.0.113.25 | Later successful MFA authentication for j.smith |
| j.smith | 8 failures followed by 1 successful authentication |
| Authentication pattern | Multiple accounts targeted within a short period |


### . Investigation Findings

Confirmed observations include repeated failed authentication attempts against multiple accounts from a common source IP.

The successful authentication against j.smith following eight failures increases investigative significance but does not establish unauthorized access.

Activity involving multiple accounts may be consistent with credential-guessing behavior. Additional evidence is required for confirmation.

### . Relevant MITRE ATT&CK Mappings

- Possible Password Guessing — T1110.001

- Possible Password Spraying — T1110.003

The mappings represent investigative hypotheses rather than confirmed adversary activity.

### . Classification and Confidence

### Classification: Suspicious / Requires Further Investigation\
Confidence: Medium\
\
. Evidence Limitations

No device information, IP reputation, geolocation, endpoint/EDR telemetry, or post-authentication activity is currently available.

Credential theft and account compromise have not been confirmed.

### . Recommended Next Investigation Actions

Further investigation should examine authentication history, MFA records, device and session information, activity associated with the source IP, authentication activity against the additional accounts, endpoint/EDR telemetry, and post-authentication activity associated with j.smith.

### Analyst Validation

The LLM-generated incident documentation accurately reflects the supplied evidence and preserves uncertainty around credential guessing, password spraying, and account compromise.

No unsupported geolocation, IP reputation, device, credential-theft, MFA-bypass, or endpoint-compromise claims were introduced.
\
Step 9 — LLM-Assisted Tier-1 to Tier-2 Escalation/Handoff

### Objective

I use an LLM to convert validated Tier-1 investigation findings into a concise Tier-2 SOC escalation/handoff.

### Scenario / Evidence:
Tier-1 Investigation Summary

### Incident: Suspicious Authentication Activity

### Severity: Medium

### Primary account: j.smith

### Additional affected accounts:

### a.lee
m.garcia
r.patel

### Authentication findings:

### - 8 failed authentications against j.smith from 198.51.100.74.

### - 1 successful authentication against j.smith from 198.51.100.74.

### - 2 failed authentications against a.lee from 198.51.100.74.

### - 1 failed authentication against m.garcia from 198.51.100.74.

### - 1 failed authentication against r.patel from 198.51.100.74.

### - j.smith later completed successful MFA authentication from 203.0.113.25.

### Correlation findings:

### - One source IP generated failed authentications against four accounts.

### - Repeated failures against j.smith were followed by successful authentication.

### - Activity occurred within a short period.

### Possible MITRE ATT&CK mappings:

### - Password Guessing — T1110.001

### - Password Spraying — T1110.003

### Current classification:

### Suspicious / Requires Further Investigation

### Confidence: Medium

### Evidence limitations:

### - No device information available.

### - No IP reputation information available.

### - No geolocation information available.

### - No endpoint/EDR telemetry available.

### - No post-authentication activity examined.

### - No confirmed credential theft.

### - No confirmed account compromise.

### Tier-1 investigation status:

### Available authentication evidence reviewed and correlated.

### Additional investigation required.

LLM Prompt:
\
Act as an AI assistant supporting a Tier-1 SOC analyst preparing

### an escalation to Tier-2 SOC.

### Create a concise professional Tier-1 to Tier-2 escalation/handoff

### from the supplied validated investigation evidence.

### Include:

### 

### 1. Escalation reason

### 2. Incident severity

### 3. Current classification and confidence

### 4. Primary affected account

### 5. Additional affected accounts

### 6. Key authentication findings

### 7. Important correlated indicators

### 8. Possible MITRE ATT&CK mappings

### 9. Investigation completed by Tier-1

### 10. Evidence still unavailable

### 11. Specific investigation requested from Tier-2

### 12. Recommended priority for continued investigation

### Requirements:

### - Use concise SOC escalation/ticket language.

### - Separate confirmed observations from possible interpretations.

### - Explain why Tier-2 investigation is required.

### - Do not claim confirmed compromise or malicious activity.

### - Do not invent evidence.

### - Do not invent IP reputation, geolocation, device, endpoint,

###  credential-theft, MFA-bypass, or post-authentication findings.

### - Preserve ATT&CK mappings as possible rather than confirmed.

### - Base the handoff only on the supplied evidence.\
\
I submitted the Scenario / Evidence and LLM Prompt to the LLM.

Step 9 — LLM-Generated Tier-1 to Tier-2 Escalation/Handoff

### Escalation Reason

Suspicious authentication activity requires additional investigation due to repeated authentication failures against multiple accounts and a subsequent successful authentication against the primary account.

### Incident Severity: Medium

### Classification and Confidence

Classification: Suspicious / Requires Further Investigation\
Confidence: Medium

### Primary Affected Account: j.smith

### Additional Affected Accounts:\
a.lee, m.garcia, r.patel

Key Authentication Findings\
j.smith experienced eight failed authentication attempts from 198.51.100.74, followed by one successful authentication from the same source.

The same source IP also generated failed authentication attempts against three additional accounts.

A later successful MFA authentication for j.smith originated from 203.0.113.25.

### Correlated Indicators

198.51.100.74 generated authentication activity against four accounts within a short period.

### The combination of multiple targeted accounts and repeated failures followed by successful authentication against j.smithwarrants further investigation.
\
Possible MITRE ATT&CK Mappings

- Password Guessing — T1110.001

- Password Spraying — T1110.003

These mappings represent possible behavioral associations and are not confirmed adversary techniques.

### Tier-1 Investigation Completed

Tier-1 analysis reviewed and correlated the available authentication events, identified activity involving multiple accounts, evaluated possible ATT&CK mappings, and classified the incident as Suspicious / Requires Further Investigation with Medium confidence.

### Evidence Still Unavailable

Device information, IP reputation, geolocation, endpoint/EDR telemetry, and post-authentication activity remain unavailable.

### Credential theft and account compromise remain unconfirmed.\
\
Tier-2 Investigation Requested

Tier-2 investigation should examine:

### Authentication and MFA history associated with j.smith\
Device and session information\
Additional activity associated with 198.51.100.74\
Authentication history for the additional affected accounts\
Endpoint/EDR telemetry associated with j.smith\
Post-authentication activity following the successful login\
Relevant identity or account-security changes\
\
Recommended Investigation Priority:

Medium priority — continued investigation recommended.

The authentication pattern warrants escalation because the available Tier-1 evidence cannot determine whether the successful authentication represents legitimate activity or unauthorized access.

### Analyst Validation

The LLM-generated handoff accurately reflects the validated Tier-1 findings and clearly identifies unresolved evidence requiring Tier-2 investigation.

No confirmed compromise, attacker identity, malicious IP reputation, geolocation, credential theft, MFA bypass, or endpoint compromise was introduced without supporting evidence.


