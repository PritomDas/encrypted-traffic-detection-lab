# encrypted-traffic-detection-lab
# Vulnerability Management Program Implementation

Implements an end-to-end enterprise vulnerability management program with Tenable/Nessus, Azure VMs, and automation scripts. Covers policy creation, scan operations, remediation workflows, and reporting for real-world security environments. In this project, we simulate the implementation of a comprehensive vulnerability management program, from inception to completion.

_**Inception State:**_ the organization has no existing policy or vulnerability management practices in place.

_**Completion State:**_ a formal policy is enacted, stakeholder buy-in is secured, and a full cycle of organization-wide vulnerability remediation is successfully completed.

---

<img width="1000" alt="image" src="./images/tenable.png">

# Technology Utilized
- Tenable (enterprise vulnerability management platform)
- Azure Virtual Machines (Nessus scan engine + scan targets)
- PowerShell & BASH (remediation scripts)

---


# Table of Contents

- [Vulnerability Management Policy Draft Creation](#vulnerability-management-policy-draft-creation)
- [Mock Meeting: Policy Buy-In (Stakeholders)](#step-2-mock-meeting-policy-buy-in-stakeholders)
- [Policy Finalization and Senior Leadership Sign-Off](#step-3-policy-finalization-and-senior-leadership-sign-off)
- [Mock Meeting: Initial Scan Permission (Server Team)](#step-4-mock-meeting-initial-scan-permission-server-team)
- [Initial Scan of Server Team Assets](#step-5-initial-scan-of-server-team-assets)
- [Vulnerability Assessment and Prioritization](#step-6-vulnerability-assessment-and-prioritization)
- [Distributing Remediations to Remediation Teams](#step-7-distributing-remediations-to-remediation-teams)
- [Mock Meeting: Post-Initial Discovery Scan (Server Team)](#step-8-mock-meeting-post-initial-discovery-scan-server-team)
- [Mock CAB Meeting: Implementing Remediations](#step-9-mock-cab-meeting-implementing-remediations)
- [Remediation Round 1: Outdated Wireshark Removal](#remediation-round-1-outdated-wireshark-removal)
- [Remediation Round 2: Insecure Protocols & Ciphers](#remediation-round-2-insecure-protocols--ciphers)
- [Remediation Round 3: Guest Account Group Membership](#remediation-round-3-guest-account-group-membership)
- [Remediation Round 4: Windows OS Updates](#remediation-round-4-windows-os-updates)
- [First Cycle Remediation Effort Summary](#first-cycle-remediation-effort-summary)

---

### Vulnerability Management Policy Draft Creation

This phase focuses on drafting a Vulnerability Management Policy as a starting point for stakeholder engagement. The initial draft outlines scope, responsibilities, and remediation timelines, and may be adjusted based on feedback from relevant departments to ensure practical implementation before final approval by upper management.  
[Draft Policy](https://docs.google.com/document/d/12l0TOK9gq2fL_bzymNfRrp8cmYW61sL2NS9_Pw4Kmak/edit?usp=sharing)


---

### Step 2) Mock Meeting: Policy Buy-In (Stakeholders)

In this phase, a meeting with the server team introduces the draft Vulnerability Management Policy and assesses their capability to meet remediation timelines. Feedback leads to adjustments, like extending the critical remediation window from 48 hours to one week, ensuring collaborative implementation.

**Pritom (Cyber Analyst):**  
*Morning, Naruto. How’ve things been lately?*

**Naruto (Server Team Manager):**  
*Hey Pritom. Busy as usual! The policy draft looks solid, but that 48-hour window for critical fixes might be tough for our team right now.*

**Pritom (Cyber Analyst):**   
*Got it. We can be flexible—how about extending it to a week, and keeping 48 hours for high-impact zero-days only?*

**Naruto (Server Team Manager):**   
*That sounds fair. Can we have a few months to settle into the new patching schedule?*

**Pritom (Cyber Analyst):**   
*Absolutely. Once we finalize the policy, all teams will get six months to adapt.*

**Naruto (Server Team Manager):**   
*Appreciate that. Thanks for looping us in—it makes the process smoother.*

**Pritom (Cyber Analyst):**  
*Of course, Naruto. We’re aiming to make this a team effort, not a top-down policy.*

**Naruto (Server Team Manager):**   
*Glad to hear that. And hey—thanks for keeping the meeting short.*

**Pritom (Cyber Analyst):**  
*Short meetings are the best kind. See you around!*

**Naruto (Server Team Manager):**   
*Later, Pritom.*

---

### Step 3) Policy Finalization and Senior Leadership Sign-Off

After gathering feedback from the server team, the policy is revised, addressing aggressive remediation timelines. With final approval from upper management, the policy now guides the program, ensuring compliance and reference for pushback resolution.  
[Final Policy](https://docs.google.com/document/d/1t1a7mbuBlKO6WmDfGt77fknW_S78n_T8K-_CNXG4he4/edit?usp=sharing)

<div style="text-align: center;">
    <img src="./images/generated-image1.png" alt="image" width="400">
</div>

---

### Step 4) Mock Meeting: Initial Scan Permission (Server Team)

The team collaborates with the server team to initiate scheduled credential scans. A compromise is reached to scan a single server first, monitoring resource impact, and using just-in-time Active Directory credentials for secure, controlled access.  

> EXPORT Initial Discovery Scan Meeting

**Pritom (Cyber Analyst):**  
*Morning, Naruto.*

**Naruto (Server Team Manager):**  
*Good morning, Pritom!*

**Pritom (Cyber Analyst):**   
*Ready to schedule some scans? Now that our vulnerability management policy is in place, I’d like to start with scheduled credential scans of your environment.*

**Naruto (Server Team Manager):** 
*Sounds good. What’s involved? How can we help?*

**Pritom (Cyber Analyst):**   
*We’re planning weekly scans of the server infrastructure. It’ll take about 4–6 hours to scan all 200 assets. We’ll need administrative credentials so the scan engine can log in remotely and check for issues.*

**Naruto (Server Team Manager):**  
*Whoa, hold on. What exactly does the scanning do? I’m worried about resource usage. Also, admin creds for all 200 machines? Isn’t that risky?*

**Pritom (Cyber Analyst):**   
*Valid concerns. The scan engine sends different traffic to servers, checks registries, looks for outdated software, insecure protocols, and weak ciphers. That’s why credentials are needed.*

**Naruto (Server Team Manager):**  
*Alright, as long as it won’t bring anything down. Let’s try it on a single server first and watch the resource usage.*

**Pritom (Cyber Analyst):**  
*Good idea. For credentials, could you set up an account in Active Directory just for us? Keep it disabled until scan time, then disable it right after—a just-in-time access approach.*

**Naruto (Server Team Manager):**  
*Sounds good. I’ll ask Susan to get the automation set up for that account.*

**Pritom (Cyber Analyst):**   
*Perfect. Talk soon!*

**Naruto (Server Team Manager):**  
*I’ll let you know when credentials are ready. See you!*

> EXPORT Vulnerability Management Policy Buy In Meeting

**Pritom (Cyber Analyst):**  
*Hey, morning Naruto. How's everything been? I know everyone's been busy lately.*

**Naruto (Server Team Manager):**  
*Good morning, Pritom. It's been hectic but we're hanging in there. Thanks for asking. I’ve read the policy draft and it mostly makes sense. But with current staffing, we can’t meet aggressive remediation timelines, especially the 48-hour window for critical vulnerabilities.*

**Pritom (Cyber Analyst):**  
*I totally understand—it is a bit aggressive, especially to start. Maybe we can extend the critical timeline to one week as a compromise, and reserve the 48-hour window only for really severe zero-day vulnerabilities.*

**Naruto (Server Team Manager):**  
*Yeah, that sounds reasonable. We appreciate the flexibility. Could we have some leeway at first as we get used to the new process? Just for the first few months?*

**Pritom (Cyber Analyst):**  
*Absolutely. After the policy is finalized, we’ll officially start the program, but all departments will have about six months to adjust and get comfortable with the new process. Does that sound fair?*

**Naruto (Server Team Manager):**  
*That works. Thanks, Pritom. We’ll do our best, and I appreciate you including us in the decision making—it really helps us feel part of the solution.*

**Pritom (Cyber Analyst):**  
*Of course—we’re all in this together. Thanks for working with us.*

**Naruto (Server Team Manager):**  
*No problem. Thanks for the short meeting.*

**Pritom (Cyber Analyst):**  
*Those are my favorite kinds. Bye now!*

**Naruto (Server Team Manager):**  
*See you later.*

---

### Step 5) Initial Scan of Server Team Assets

In this phase, an insecure Windows Server is provisioned to simulate the server team's environment. After creating vulnerabilities, an authenticated scan is performed, and the results are exported for future remediation steps.  

<img width="635" alt="image" src="./images/initialscan-image2.png" style="border: 2px solid black;">

[Scan 1 - Initial Scan](https://drive.google.com/file/d/1iXtH9wYF3qrXFzfk7iZuhFW2NyajDsHz/view?usp=sharing)




---

### Step 6) Vulnerability Assessment and Prioritization

We assessed vulnerabilities and established a remediation prioritization strategy based on ease of remediation and impact. The following priorities were set:

1. Third Party Software Removal (Wireshark)
2. Windows OS Secure Configuration (Protocols & Ciphers)
3. Windows OS Secure Configuration (Guest Account Group Membership)
4. Windows OS Updates

---

### Step 7) Distributing Remediations to Remediation Teams

The server team received remediation scripts and scan reports to address key vulnerabilities. This streamlined their efforts and prepared them for a follow-up review.  

<img width="635" alt="image" src="./images/remediationemail-image3.png">

[Remediation Email](https://github.com/PritomDas/enterprise-vulnerability-management-with-tenable/blob/main/misc/remediation-email.md)

---

### Step 8) Mock Meeting: Post-Initial Discovery Scan (Server Team)

The server team reviewed vulnerability scan results, identifying outdated software, insecure accounts, and deprecated protocols. The remediation packages were prepared for submission to the Change Control Board (CAB). 

**Pritom (Cyber Analyst):**  
*Morning, Naruto. How are you doing?*

**Naruto (Server Team Manager):**  
*Not bad for a Monday. And you?*

**Pritom (Cyber Analyst):**  
*Still alive, so I can't complain! Before we get into the vulnerabilities—how did the scan go? Any outages or resource issues?*

**Naruto (Server Team Manager):**  
*The scan went well. We were monitoring everything, and aside from a lot of open connections, we barely noticed the scan.*

**Pritom (Cyber Analyst):**  
*That's great news. As expected! We'll keep monitoring, but I don't anticipate any utilization issues. Mind if I jump into the vulnerability findings?*

**Naruto (Server Team Manager):**  
*Go for it.*

**Pritom (Cyber Analyst):**  
*Most vulnerabilities are from outdated Wireshark installs—lots of old versions detected. One odd thing: the local guest account is part of the local administrators group on some servers. That might need a closer look. A few vulnerabilities might be auto-fixed by regular Windows Updates, like the Microsoft Edge one. The self-signed certificate warning isn’t urgent. But the medium-strength cipher suites and old TLS 1.1/1.0 protocols are deprecated and need remediation.*

**Naruto (Server Team Manager):**  
*Interesting. I suspect most servers will have similar issues, which could simplify remediation.*

**Pritom (Cyber Analyst):**  
*Exactly—a consistent set of issues makes rollout easier. Do you foresee any problems with fixing these, especially the cipher suites and protocols?*

**Naruto (Server Team Manager):**  
*Not really. We’ll get them approved in the next Change Control Board. Removing Wireshark and fixing the guest account should be straightforward—I’ll follow up with our CIS admins.*

**Pritom (Cyber Analyst):**  
*Sounds good. I’ll start building remediation packages for you to deploy. By the way, do you already have something in place for patching Windows Update vulnerabilities?*

**Naruto (Server Team Manager):**  
*Yes, patch management is handled automatically. Should be up to date by next week.*

**Pritom (Cyber Analyst):**  
*Perfect. I’ll get started on remediation strategies and follow up before the next Change Control Board.*

**Naruto (Server Team Manager):**  
*Sounds good. Talk to you soon!*

**Pritom (Cyber Analyst):**  
*Talk soon!*


---

### Step 9) Mock CAB Meeting: Implementing Remediations

The Change Control Board (CAB) reviewed and approved the plan to remove insecure protocols and cipher suites. The plan included a rollback script and a tiered deployment approach.  

**CAB Facilitator:**  
*Next on the agenda: review and approval for removing insecure protocols and cipher suites from our servers. Pritom from VM Security, could you walk us through the technical details?*

**Pritom (VM Sec Analyst):**  
*Absolutely. We’ve identified that several of our servers still have deprecated protocols and weak cipher suites enabled, which leaves us exposed to legacy security risks. The solution is pretty straightforward—we’re running a PowerShell script that disables those insecure protocols and ciphers using registry updates, so only secure, modern algorithms are available. It’s a simple but important change for compliance and reducing risk.*

**CAB Facilitator:**  
*Thanks, Pritom. If something goes wrong after rollout—say, if a production server fails or needs those old protocols for an app—do we have a rollback plan?*

**Pritom (VM Sec Analyst):**  
*Definitely. We’ve designed the deployment to occur in three phases: pilot group, pre-production, then full production. At each phase, we’ll monitor, and we have an automated rollback script that restores the previous registry settings if anything unexpected happens. That means minimal risk to operations.*

**CAB Facilitator:**  
*So these are only registry-level changes, no deeper application impact?*

**Pritom (VM Sec Analyst):**  
*Exactly—just registry updates, targeting system-level cryptography settings. No app code or user changes.*

**CAB Facilitator:**  
*Are there any concerns about platform dependencies or edge cases you haven’t tested?*

**Pritom (VM Sec Analyst):**  
*We’ve validated the scripts in test and QA environments mirroring production, and confirmed support with Microsoft’s documentation for Windows server cryptography. If anything unusual appears in pilot, we’ll pause and investigate before moving forward.*

**CAB Facilitator:**  
*Great. Any other questions from the team?*

*(silent, then general agreement)*

**CAB Facilitator:**  
*All right—we’re approving the tiered deployment as described, with contingency plans in place. Thanks for the thorough presentation, Pritom. Let’s move forward on this one!*

---
### Step 10 ) Remediation Effort

**Remediation Round 1: Outdated Wireshark Removal**

The server team used a PowerShell script to remove outdated Wireshark. A follow-up scan confirmed successful remediation.  
[Wireshark Removal Script](https://github.com/PritomDas/enterprise-vulnerability-management-with-tenable/blob/main/automation%20scripts/remediation-wireshark-uninstall.ps1)  

<img width="634" alt="image" src="./images/wiresharkremoval-image4.png">

[Scan 2 - Third Party Software Removal](https://drive.google.com/file/d/129K-7lz_mAOnKW9L2M8HNdbcOJGlw10i/view?usp=sharing)


**Remediation Round 2: Insecure Protocols & Ciphers**

The server team used PowerShell scripts to remediate insecure protocols and cipher suites. A follow-up scan verified successful remediation, and the results were saved for reference.  
[PowerShell: Insecure Protocols Remediation](https://github.com/PritomDas/enterprise-vulnerability-management-with-tenable/blob/main/automation%20scripts/toggle-protocols.ps1)
[PowerShell: Insecure Ciphers Remediation](https://github.com/PritomDas/enterprise-vulnerability-management-with-tenable/blob/main/automation%20scripts/toggle-cipher-suites.ps1)

<img width="630" alt="image" src="./images/protocolremoval-image5.png">

[Scan 3 - Ciphersuites and Protocols](https://drive.google.com/file/d/1nOI6jmehj0s6AjGBEIQ8WKGojhVcTqYZ/view?usp=sharing)


**Remediation Round 3: Guest Account Group Membership**

The server team removed the guest account from the administrator group. A new scan confirmed remediation, and the results were exported for comparison.  
[PowerShell: Guest Account Group Membership Remediation](https://github.com/PritomDas/enterprise-vulnerability-management-with-tenable/blob/main/automation%20scripts/toggle-guest-local-administrators.ps1)  

<img width="627" alt="image" src="./images/guestaccountremove-image6.png">

[Scan 4 - Guest Account Group Removal](https://drive.google.com/file/d/1wWSibuxdl4R9Z4iq7Fwx-xLi2unaZn0c/view?usp=sharing)


**Remediation Round 4: Windows OS Updates**

Windows updates were re-enabled and applied until the system was fully up to date. A final scan verified the changes  

<img width="627" alt="image" src="./images/windowsosupdates-image7.png">

[Scan 5 - Post Windows Updates](https://drive.google.com/file/d/1BUD3HWEUMR6Q6dnbrijvA9HhyqcAyV50/view?usp=sharing)

---

### First Cycle Remediation Effort Summary

The remediation process reduced total vulnerabilities by 80%, from 30 to 6. Critical vulnerabilities were resolved by the second scan (100%), and high vulnerabilities dropped by 90%. Mediums were reduced by 76%. In an actual production environment, asset criticality would further guide future remediation efforts.  

<img width="1920" alt="image" src="./images/scantrend-image8.png">

[Remediation Data](https://docs.google.com/spreadsheets/d/1TvLusPLI-sgPvyMMxvBRoMl8mLiiokmuLHDND5t-_28/edit?usp=sharing)

---

### On-going Vulnerability Management (Maintenance Mode)

After completing the initial remediation cycle, the vulnerability management program transitions into **Maintenance Mode**. This phase ensures that vulnerabilities continue to be managed proactively, keeping systems secure over time. Regular scans, continuous monitoring, and timely remediation are crucial components of this phase. (See [Finalized Policy](https://docs.google.com/document/d/1t1a7mbuBlKO6WmDfGt77fknW_S78n_T8K-_CNXG4he4/edit?usp=sharing) for scanning and remediation cadence requirements.)

Key activities in Maintenance Mode include:
- **Scheduled Vulnerability Scans**: Perform regular scans (e.g., weekly or monthly) to detect new vulnerabilities as systems evolve.
- **Patch Management**: Continuously apply security patches and updates, ensuring no critical vulnerabilities remain unpatched.
- **Remediation Follow-ups**: Address newly identified vulnerabilities promptly, prioritizing based on risk and impact.
- **Policy Review and Updates**: Periodically review the Vulnerability Management Policy to ensure it aligns with the latest security best practices and organizational needs.
- **Audit and Compliance**: Conduct internal audits to ensure compliance with the vulnerability management policy and external regulations.
- **Ongoing Communication with Stakeholders**: Maintain open communication with teams responsible for remediation, ensuring efficient coordination.

By maintaining an active vulnerability management process, organizations can stay ahead of emerging threats and ensure long-term security resilience.

