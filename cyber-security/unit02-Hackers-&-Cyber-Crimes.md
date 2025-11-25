

## 😈 Cyber Security Study Notes: 
## 🚨 Unit 2 - Hackers and Cyber Crimes (Emoji Enhanced)

---

## 1. 🧑‍💻 Types of Hackers, Hackers, and Crackers

### Introduction
The key difference between hacker types lies in their **intent** and **ethics**—the community categorizes them using a "hat" system.

### Core Concepts and Definitions
#### A. Types of Hackers (The Hat System)
| Type | Hat Color | Intent/Ethics | Role/Action |
| :--- | :--- | :--- | :--- |
| **White Hat Hacker** | ⚪ 😇 | **Ethical and Legal**. | Works for organizations; finds vulnerabilities to **fix** them. Operates with explicit permission (e.g., Penetration Testers). |
| **Black Hat Hacker** | ⚫ 😈 | **Malicious and Illegal**. | Exploits vulnerabilities for personal gain, theft, sabotage, or to cause damage. Operates without permission. |
| **Grey Hat Hacker** | ⚖️ 🤷 | **Borderline Ethics**. | Finds vulnerabilities without permission, then reports them (sometimes for a fee). Breaks laws but typically without malicious intent. |

#### B. Hacker vs. Cracker
This distinction clarifies intent:
* **Hacker:** Used neutrally or positively (White Hat); refers to someone with advanced technical skills.
* **Cracker:** **Always** refers to a **malicious** individual (**Black Hat**) who attempts to illegally break into a system to steal, corrupt, or disrupt data, often focusing on bypassing software protections.

### Real-life Examples or Analogies
* 💰 **Black Hat:** A criminal group using **ransomware** to encrypt a hospital's files.
* 🛡️ **White Hat:** A security consultant hired by a company to try and breach their system to test defenses.

### Tips to Memorize
* 🧠 **Mnemonic:** Remember the colors and their meaning: **White** = Good/Lawful, **Black** = Evil/Criminal, **Grey** = In-between/Ambiguous.

---

## 2. 🚨 Cyber-Attacks and Vulnerabilities

### Introduction
A **Cyber-Attack** is an attempt to gain unauthorized access. This is only possible due to a **Vulnerability**—a pre-existing weakness in the system.

### Core Concepts and Definitions
#### A. Vulnerability
* **🔍 Definition:** A **weakness** in a system, application, network, or process that can be **exploited** by a threat actor.
* **Types:**
    * 🐞 **Software Flaws:** Bugs or errors in code (e.g., buffer overflow).
    * ⚙️ **Configuration Errors:** Default passwords, open ports.
    * 🧑‍🤝‍🧑 **Human Errors:** Weak passwords, susceptibility to social engineering.
* **🔑 Zero-Day:** A critical vulnerability that is **unknown** to the software vendor (and thus unpatched) at the time it is actively being exploited.

#### B. Cyber Attack
* **💥 Definition:** The act of using a **threat** (the danger) to **exploit** a **vulnerability** (the weakness) to cause harm.
* **Attack Triad:**
    1.  **Threat** (Potential Danger, e.g., Hacker)
    2.  **Vulnerability** (Weakness, e.g., Unpatched Server)
    3.  **Risk** (Likelihood of Harm)
* **Common Attack Examples:**
    * 🌊 **DDoS:** Overwhelming a server with huge volumes of traffic to shut it down.
    * 🎣 **Phishing:** Tricking users via deceptive emails to steal credentials.
    * 💾 **SQL Injection:** Inserting malicious code into input fields to access/modify a database.

### Common Mistakes to Avoid
* ❌ **Mistake:** Confusing **Vulnerability** (the weakness) with **Exploit** (the tool).
* ✅ **Correction:** The vulnerability is the **locked window left open**; the exploit is the **ladder** the thief uses to climb in.

---

## 3. 🦠 Malware Threats

### Introduction
**Malware** (Malicious Software) is the primary tool of cybercrime, designed to cause harm or gain unauthorized access.

### Core Concepts and Definitions
| Malware Type | Icon | Action/Purpose | Tip to Memorize |
| :--- | :--- | :--- | :--- |
| **Virus** | 🐞 | Attaches to a legitimate program (**host file**); spreads when the host is **executed** (requires user action). | **V**ery **R**equires **U**ser **S**tart. |
| **Worm** | 🐛 | **Self-propagating** and **self-replicating**. Spreads independently across networks without needing a host or user action. | **W**anders **O**n **R**andom **M**achines. |
| **Trojan Horse** | 🐎 | **Disguises** itself as legitimate software (e.g., a free game) but contains a malicious payload. | Looks **Troj**an like, acts malicious. |
| **Ransomware** | 🔒 | **Encrypts** a victim's files, demanding a ransom (usually in crypto) for the decryption key. | Holds data **Ransom**. |
| **Spyware** | 👁️ | Secretly **monitors** user activity (keystrokes, screenshots) and reports data back to the attacker. | **Spy**ing on the user. |
| **Rootkit** | 💀 | Designed to **hide** the existence of other malware and maintain privileged **root** access to the system. | Gives the attacker the **Root** of power. |

### Real-life Examples
* 💸 **Ransomware:** The **WannaCry** attack that encrypted systems globally.
* 🚪 **Trojan:** A fake login prompt that, once clicked, installs a **Backdoor**.

---

## 4. 🚀 Cyber Attack Lifecycle: Execution and Evasion Techniques

### Introduction
The lifecycle moves from initial access to full control and finally, evasion (covering tracks).

### A. The Attack Stages (Gaining Access & Privilege Escalation)
* **🕵️ Sniffing (Reconnaissance):**
    * **Action:** Intercepting and inspecting network traffic (**data packets**) traveling over a channel.
    * **Goal:** To capture credentials (if unencrypted) or map the network structure.
* **🔓 Gaining Access (Exploitation):**
    * **Action:** Using an **exploit** to take advantage of a **vulnerability** to gain an initial foothold.
    * **Result:** Attacker gets **low-level user access**.
* **⏫ Escalating Privileges (Post-Exploitation):**
    * **Action:** Moving from initial low-level access to a higher level, such as **Administrator** or **Root**.
    * **Goal:** To gain complete control over the system (install malware, change settings).

### B. Evasion and Persistence (Hiding Files & Covering Tracks)
* **⚙️ Executing Applications:**
    * With high privileges, the attacker executes key applications like a **rootkit** or a **backdoor** to ensure persistent access.
    * **Backdoor:** A secret method of bypassing normal authentication or encryption to gain remote access to a program or system.
* **🫥 Hiding Files:**
    * **Action:** Making malicious files and tools invisible to normal users and security software.
    * **Method:** Using **Rootkits** to modify operating system core files to omit attacker files/processes from directory listings.
* **🧹 Covering Tracks (Anti-Forensics):**
    * **Action:** Eliminating evidence of the attack to prevent detection and forensic analysis.
    * **Methods:** Clearing system logs (Event Viewer, Bash history), deleting temporary files, and using memory-only malware.

### Tips to Memorize
* 🗺️ **Keywords Sequence:** **S**niffing (Look) $\to$ **G**aining **A**ccess (Enter) $\to$ **E**scalating **P**rivileges (Get Keys) $\to$ **H**iding **F**iles (Hide) $\to$ **C**overing **T**racks (Erase).

---
