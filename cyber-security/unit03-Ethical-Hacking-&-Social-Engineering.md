## 🧠 Cyber Security Study Notes
## 🛡️ Unit 3 - Ethical Hacking and Social Engineering 

---

## 1. 😇 Ethical Hacking Concepts and Scopes

### Introduction
**Ethical Hacking** is the authorized practice of testing a system's security defenses by attempting to breach them, exactly like a Black Hat hacker, but with the explicit goal of identifying and fixing vulnerabilities. It’s an essential part of a mature security posture.

### Core Concepts and Definitions
* **📜 Ethical Hacking Definition:** The process of trying to bypass system security measures using the same tools and techniques as malicious attackers, but in a **legal and ethical manner** (White Hat).
* **🎯 Goal:** To assess the security posture of an organization, discover **vulnerabilities**, and provide recommendations to remediate them *before* they can be exploited.
* **Scope of Ethical Hacking:**
    * **Network Penetration Testing (External/Internal):** Testing firewalls, routers, and internal network devices.
    * **Web Application Penetration Testing:** Testing website logic, input validation, and server-side code.
    * **Wireless Security Testing:** Assessing Wi-Fi setup and authentication mechanisms.
    * **Social Engineering Testing:** Attempting to trick employees to test awareness.
    * **Physical Security Testing:** Assessing physical access controls (doors, cameras, locks).

### Ethical Hacking Phases (A Formal Process)
1.  **👣 Reconnaissance:** Gathering preliminary information about the target system (e.g., domain names, IP addresses, employee details).
2.  **🔍 Scanning:** Using tools (like Nmap) to find open ports, services, and operating system types.
3.  **🔓 Gaining Access:** Exploiting vulnerabilities found during scanning to get a low-level foothold.
4.  **⏫ Maintaining Access:** Installing backdoors or rootkits to ensure long-term, persistent access (simulated).
5.  **🧹 Covering Tracks:** Erasing log files and traces of the attack (simulated).
6.  **📝 Reporting:** Documenting all vulnerabilities, exploits, and providing remediation strategies (the most crucial phase).

### Important Keywords
* **Keywords:** Rules of Engagement (RoE), Penetration Testing (Pen Test), Bug Bounty, Vulnerability Disclosure.

### Common Mistakes to Avoid
* ❌ **Mistake:** Starting an Ethical Hack without a clear, written **Rules of Engagement (RoE)** document and legal permission.
* ✅ **Correction:** Always ensure you have **explicit, signed permission** to test, specifying the scope, timing, and limits of the test.

---

## 2. 💣 Threats and Attack Vectors, and Information Assurance

### Introduction
Understanding the pathways an attacker uses (**Attack Vectors**) and the potential dangers (**Threats**) allows us to focus on the overall defense philosophy (**Information Assurance**).

### Core Concepts and Definitions
#### A. Threats and Attack Vectors
* **Threat:** A potential danger or actor that could exploit a vulnerability (e.g., a Black Hat, a natural disaster).
* **Attack Vector:** The pathway or method used by a threat actor to gain unauthorized access to an asset.
    * **💻 Network Vector:** Exploiting open ports, outdated firewalls, or network protocols (e.g., DDoS).
    * **📧 Software/Application Vector:** Exploiting bugs in code, configuration errors, or using SQL injection.
    * **🧑‍🤝‍🧑 Human Vector (Social Engineering):** Phishing emails, pretexting, or tailgating.
    * **🔌 Physical Vector:** Unauthorized access to a server room or installation of a malicious device (e.g., keylogger).

#### B. Information Assurance (IA)
* **🛡️ Definition:** The practice of managing risks related to the use, processing, storage, and transmission of information systems and data. It's a broader term than cybersecurity.
* **Goal:** To ensure the **CIA Triad** and additional concepts like **Authentication** and **Non-Repudiation**.
    * **Authentication:** Verifying the user's identity (Are you who you say you are?).
    * **Non-Repudiation:** Ensuring that a party cannot successfully deny the authorship of a document or the fact that they performed an action (Proof of origin/delivery).
* **IA vs. Cyber Security:** IA focuses on the management of information risk and controls across the entire organization (governance and policy), while Cyber Security is focused on the technical implementation of those controls.

### Tips to Memorize
* **IA Components Mnemonic:** Remember **CIA+AN**: **C**onfidentiality, **I**ntegrity, **A**vailability + **A**uthentication, **N**on-Repudiation.

---

## 3. 🗺️ Threat Modelling and Enterprise Information Security Architecture (EISA)

### Introduction
These concepts move security from a reactive fix to a **proactive, design-level discipline**.

### Core Concepts and Definitions
#### A. Threat Modelling
* **🏗️ Definition:** A structured process for identifying, quantifying, and communicating security risks associated with an application, network, or business process. It is done **during the design phase** (Shift-Left Security).
* **Purpose:** To understand **where** the system is vulnerable and what the potential impact of an attack would be.
* **Common Methodologies (STRIDE):**
    * **S**poofing (Impersonation)
    * **T**ampering (Integrity violation)
    * **R**epudiation (Non-Repudiation failure)
    * **I**nformation Disclosure (Confidentiality violation)
    * **D**enial of Service (Availability violation)
    * **E**levation of Privilege (Authorization failure)

#### B. Enterprise Information Security Architecture (EISA)
* **🏢 Definition:** The set of documented structural artifacts (models, principles, and policies) that define how the entire organization's information and technology assets are secured.
* **Goal:** To align the organization's security strategy with its business strategy, ensuring a unified, effective, and cost-efficient security posture across all departments (Governance).
* **Key Principle:** **Defense-in-Depth**—using multiple layers of security controls (perimeter, network, host, application, data) so that if one layer fails, others still offer protection.

### Summary or Revision Points (Comparative Table)
| Concept | Focus | When Used | Goal |
| :--- | :--- | :--- | :--- |
| **Threat Modelling** | Individual Application/System | Design Phase (Proactive) | Identify and mitigate design-level security flaws. |
| **EISA** | Entire Organization/Business | Strategic Planning | Ensure security aligns with business goals and is consistently applied (Governance). |

---

## 4. 📝 Vulnerability Assessment and Penetration Testing

### Introduction
These are the two most common technical methods used by Ethical Hackers to evaluate the security of an asset. They are often confused but have distinct goals.

### Core Concepts and Definitions
#### A. Vulnerability Assessment (VA)
* **🔍 Definition:** An automated process of scanning systems and applications for known weaknesses using commercial or open-source tools.
* **Goal:** To provide a **comprehensive list** of security flaws and rank them by severity (High, Medium, Low).
* **Characteristics:**
    * **Non-Intrusive:** Doesn't exploit the vulnerabilities; only identifies them.
    * **Broad Coverage:** Tests for a wide array of known issues (signatures).
    * **Result:** A **Vulnerability Report** (list of risks).

#### B. Penetration Testing (Pen Test)
* **⚔️ Definition:** A hands-on, simulated attack where a human ethical hacker attempts to **exploit** vulnerabilities to prove whether they can gain unauthorized access and what the business impact would be.
* **Goal:** To prove **exploitability** and measure the real-world risk.
* **Characteristics:**
    * **Intrusive/Targeted:** Attempts to break in; focuses on chaining multiple low-level vulnerabilities together.
    * **Narrower Scope:** Focuses on proving access to a specific goal.
    * **Result:** A **Proof-of-Concept** and an **Exploitation Report** (what happened after the breach).

### Pen Test Types (By Knowledge Level)
* **⚪ White Box:** Tester has full knowledge of the system (source code, architecture). **Simulates an Insider Attack.**
* **⚫ Black Box:** Tester has no prior knowledge, only publicly available information. **Simulates an External Attacker.**
* **⚖️ Grey Box:** Tester has some limited knowledge (e.g., a standard user account and network diagrams).

---

## 5. 🎣 Social Engineering, Insider Attacks, and Defense

### Introduction
Social Engineering exploits the **human factor**—the weakest link in the security chain—and is the basis for many successful breaches.

### Core Concepts and Definitions
#### A. Types of Social Engineering
* **📧 Phishing:** Using fraudulent emails to trick a recipient into revealing sensitive information or clicking a malicious link.
* **🎯 Spear Phishing:** Phishing attack highly targeted at a specific individual or organization.
* **📞 Vishing (Voice Phishing):** Using phone calls (voice) to trick victims (e.g., pretending to be IT support).
* **🚶 Tailgating/Piggybacking:** Following an authorized person through a secure access point (e.g., holding the door).
* **🎭 Pretexting:** Creating a fake scenario or "pretext" to gain trust and information (e.g., claiming to be a building inspector).

#### B. Insider Attack
* **👤 Definition:** A malicious or negligent attack carried out by a current or former employee, contractor, or business associate who has (or had) authorized access to the organization’s network or data.
* **Threat Types:**
    * **Malicious Insider:** Intentionally steals data or sabotages systems for revenge or profit.
    * **Negligent Insider:** Unintentionally causes a breach (e.g., clicking a phishing link, losing a company laptop).

#### C. Social Engineering Targets and Defence Strategies
* **Targets:** Individuals with access to sensitive data (System Admins, Finance Staff, Executives) or weak awareness.
* **🛡️ Defence Strategies:**
    * **1. Security Awareness Training:** Mandatory, regular training on how to spot phishing, vishing, and tailgating.
    * **2. Least Privilege Principle:** Users should only have the minimum permissions necessary to perform their job (limits damage from a compromised account).
    * **3. Multi-Factor Authentication (MFA):** Requires a second verification step (e.g., a code from a phone) even if the password is stolen via phishing.

### Preventing Insider Threats
* **🔒 Access Control:** Strictly enforce the principle of Least Privilege and review access rights regularly (especially after role changes).
* **👀 Monitoring:** Implement monitoring tools (e.g., DLP - Data Loss Prevention) to track unusual file access, mass downloads, or sensitive data transfer.
* **👋 Exit Procedure:** Immediately revoke all system access and collect all company assets (laptops, badges) upon an employee's departure.

### Summary or Revision Points
* **Social Engineering:** Exploits **humans** (Phishing, Pretexting).
* **Insider Threat:** Caused by **trusted individuals** (Malicious or Negligent).
* **Defense Focus:** **Training**, **MFA**, and **Least Privilege**.