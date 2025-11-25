## 🕵️ Cyber Security Study Notes
## 🔍 Cyber Forensics and Auditing


---

## 1. 🔬 Introduction to Cyber Forensics

### Introduction
**Cyber Forensics** (or Digital Forensics) is the science of locating, collecting, preserving, analyzing, and presenting evidence found on digital media in a manner that is **legally admissible** in a court of law. It is crucial for **post-incident analysis** and criminal prosecution.

### Core Concepts and Definitions
* **💻 Cyber Forensics Definition:** The process of acquiring and analyzing electronic data while maintaining the integrity of the data chain of custody.
* **🎯 Goal:** To reconstruct the timeline of an incident, identify the attacker, determine the method of attack, and provide factual evidence for legal proceedings.
* **Key Principle: Chain of Custody:** The chronological documentation (paper trail) showing the seizure, custody, control, transfer, analysis, and disposition of physical and electronic evidence. Maintaining this is **non-negotiable** for evidence admissibility.
* **Forensic Image (Disk Image):** A bit-for-bit, sector-by-sector identical copy of the original storage media. Analysis is always performed on this image, **never** on the original evidence.

### Computer Equipment and Associated Storage Media
Cyber forensics covers any device that can store data:
* **🖥️ Computer Systems:** Hard Disk Drives (HDDs), Solid State Drives (SSDs), RAM (Volatile Memory), Motherboard chips.
* **📱 Mobile Devices:** Internal storage, SIM cards, SD cards.
* **☁️ Network & Cloud:** Server logs, Firewall logs, Router configurations, Cloud storage snapshots.
* **💾 Removable Media:** USB drives, CDs/DVDs.

### Tips to Memorize
* **Forensics Sequence:** **A**cquisition $\to$ **P**reservation $\to$ **A**nalysis $\to$ **R**eporting (**APAR**).

---

## 2. 🧑‍⚖️ Role of Forensics Investigator and Investigation Process

### Introduction
The **Forensics Investigator** acts as the technical detective and expert witness, guiding the entire process meticulously to avoid contaminating evidence.

### Role of Forensics Investigator
* **🔍 Evidence Triage:** Quickly determining the priority of evidence collection (e.g., volatile memory first).
* **🔒 Secure Handling:** Ensuring the original evidence is write-protected or secured to prevent alteration.
* **🧪 Objective Analysis:** Performing unbiased analysis using validated tools and methodologies.
* **🗣️ Expert Witness:** Testifying in court about the findings and the methods used.
* **📚 Documentation:** Detailed logging of every step, tool, and action taken to maintain the Chain of Custody.

### Forensics Investigation Process (The Seven Steps)
1.  **Preparation:** Securing legal authorization and preparing the tool kit (write blockers, forensic software).
2.  **Identification:** Identifying the incident (what happened?) and the digital sources of evidence.
3.  **Collection/Acquisition:** Collecting the evidence, starting with **volatile data** (like RAM) and then **non-volatile data** (disk image).
4.  **Preservation:** Securing the evidence using techniques like **write-blocking** and creating a forensic image. Hashing the image (e.g., SHA-256) to ensure integrity.
5.  **Analysis:** Examining the collected data for artifacts, files, registry keys, and timeline reconstruction.
6.  **Documentation:** Logging all tools, methods, and findings in detail.
7.  **Reporting:** Generating a comprehensive, clear report suitable for technical teams and legal entities.

### Collecting Network Based Evidence
* **Logging is Key:** Network devices (routers, firewalls, IDS/IPS) must be configured to log traffic and events.
* **Types of Evidence:**
    * **Flow Data (NetFlow/IPFIX):** Records who talked to whom, when, and how much data was transferred (metadata).
    * **Packet Capture (PCAP):** Full capture of the actual data packets for deep analysis.
    * **Device Logs:** Logs from routers, firewalls, and proxy servers showing connection attempts, rejected packets, and access requests.
* **Challenge:** Network data is often **ephemeral** (short-lived) or massive, requiring powerful storage and filtering techniques.

### Writing Computer Forensics Reports
A forensics report must be:
* **✅ Factual:** Based only on analyzed data, not assumptions.
* **📝 Complete:** Including the entire methodology, tools used, and chain of custody documentation.
* **🔎 Clear:** Written in clear language, defining technical terms for non-technical audiences (judges, lawyers).
* **🎯 Focused:** Answering specific questions related to the incident.

---

## 3. 📊 Auditing and Information Security Management System (ISMS)

### Introduction
**Auditing** is a formal, independent process used to evaluate an organization's security controls and compliance against a specific standard or set of criteria.

### Core Concepts and Definitions
* **⚖️ Auditing Definition:** A systematic, independent, and documented process for obtaining audit evidence and evaluating it objectively to determine the extent to which audit criteria are fulfilled.
* **Purpose:** To provide assurance to stakeholders (management, customers, regulators) that security controls are effective and compliance requirements are met.
* **Types of Audits:**
    * **Internal Audit:** Performed by employees for internal assurance (self-check).
    * **External Audit:** Performed by independent third parties for certification (e.g., ISO 27001).
    * **Compliance Audit:** Checking adherence to regulations (e.g., HIPAA, GDPR).

### Plan an Audit Against a Set of Audit Criteria
The auditing process is systematic:
1.  **Preparation:** Define the **Audit Criteria** (the standard being measured against, e.g., ISO 27001). Define the scope (which systems, departments).
2.  **Execution:** Gather evidence through interviews, document reviews, and technical testing.
3.  **Review:** Compare the evidence against the audit criteria. Identify **non-conformities** (gaps).
4.  **Reporting:** Document findings, focusing on non-conformities and suggested **Corrective Actions**.

### Information Security Management System (ISMS) Management
* **🛡️ ISMS Definition:** A set of policies, procedures, and systems that manage an organization's sensitive data risks. It is a systematic approach to continually manage and protect company and customer information.
* **Key Components (Based on PDCA Cycle):**
    * **Plan (P):** Establish the ISMS policy, objectives, and controls (Risk Assessment).
    * **Do (D):** Implement and operate the controls.
    * **Check (C):** Monitor, review, and audit the ISMS (Internal Audits).
    * **Act (A):** Maintain and improve the ISMS based on audit results.

### Introduction to ISO 27001:2013
* **🌟 ISO 27001:** The international standard that specifies the requirements for establishing, implementing, maintaining, and continually improving an **ISMS**.
* **Goal:** To help organizations make the information assets they hold secure, managing risk effectively.
* **Key Element:** Requires a systematic approach to risk management, including identifying risks, assessing them, and treating them with appropriate controls (security measures).
* **Annex A:** The crucial section containing a list of **114 specific security controls** (e.g., access control, physical security, cryptography) that organizations must consider implementing based on their risk assessment.

### Summary or Revision Points (Mind Map Keywords)
* **Forensics:** Legal Admissibility, Chain of Custody, Write Blocker, Volatile Data, APAR.
* **Auditing:** Criteria, Non-Conformity, Assurance, ISMS (PDCA).
* **ISO 27001:** International Standard, ISMS Requirements, Risk Management, Annex A Controls.