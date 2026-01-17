# 📚 Unit 1 

## 🛑 1. Introduction & Need for Security 🛡️

**Exam Weight:** ⭐⭐⭐ (Commonly asked as a 5-mark introductory question)

### Introduction

In today’s digital age, data is the new oil. **Computer Security** is the protection of computer systems and information from harm, theft, and unauthorized use. It’s not just about passwords; it's about ensuring that the entire ecosystem (hardware, software, and data) remains safe.

### Why do we need Security? 🚩

With the rise of the internet, the "surface area" for attacks has increased. Here is why security is mandatory:

* **Protection of Sensitive Data:** To keep personal info (credit card details, medical records) private. 💳
* **Preventing Financial Loss:** Cyber-attacks can lead to direct theft or massive recovery costs. 💸
* **Maintaining Reputation:** For companies, a data breach means a loss of customer trust. 🤝
* **Resource Availability:** To ensure that systems are up and running when needed (preventing crashes). 📉

### Real-life Analogy 🏠

Think of your computer like a **house**.

* **Need for Security:** You have valuables inside (Data).
* **The Threat:** Burglars (Hackers).
* **The Defense:** Locks (Passwords), Alarms (Firewalls), and CCTV (Intrusion Detection).

---

## 🏛️ 2. Security Approaches (Security Models) 🏗️

**Exam Weight:** ⭐⭐⭐⭐ (Important for understanding the 'how' of security)

Security isn't a single "tool"; it's a strategy. There are three main approaches used in the industry:

### 1. Trusted Systems Approach 🔒

This approach focuses on building a system that is inherently secure. The OS (Operating System) itself controls who can access what.

* **Pros:** Very high security.
* **Cons:** Expensive and complex to build.

### 2. Security Perimeter Approach 🏰

This is like building a high wall around a castle. You focus on the **edges** of the network (Firewalls, Routers).

* **Pros:** Good for keeping outsiders away.
* **Cons:** If an attacker gets "inside" the wall, the system is defenseless.

### 3. Layered Approach (Defense in Depth) 🧅

This is the most modern approach. Like an onion, you have multiple layers of security. If one fails, the next one protects the data.

* **Layers include:** Physical security -> Network security -> Host security -> Application security -> Data security.

> **💡 Exam Tip:** Always draw the "Onion Model" for a 10-mark answer on security approaches.

---

## ⚖️ 3. Principles of Security (The CIA Triad) 🔑

**Exam Weight:** ⭐⭐⭐⭐⭐ (Most Frequently Asked - Essential for 10-mark answers)

Every security mechanism is built on these three (plus two extra) pillars.

### The CIA Triad

| Principle | Definition (Simple Terms) | Example of a Failure |
| --- | --- | --- |
| **Confidentiality** 🤫 | Only authorized people can read the data. | A hacker steals your password. |
| **Integrity** ✅ | Data should not be changed by unauthorized people during transit. | Someone changes the amount on a digital cheque from $10 to $1000. |
| **Availability** 🕒 | Data and services must be accessible when needed. | A website crashes because of a DDoS attack. |

### Additional Principles

* **Authentication:** Proving you are who you say you are (ID cards, Biometrics). 🆔
* **Non-Repudiation:** Ensuring that a sender cannot later deny sending a message. (Digital Signatures). ✍️

### 🧠 Mnemonic to Remember: **"C-I-A"**

Just remember the American intelligence agency! **C**onfidentiality, **I**ntegrity, **A**vailability.

---

## ⚔️ 4. Types of Attacks 👾

**Exam Weight:** ⭐⭐⭐⭐⭐ (High probability of appearing in Part B - 10 Marks)

Attacks are generally classified into two main categories: **Passive** and **Active**.

### A. Passive Attacks (The "Eavesdropper") 👂

The goal of the attacker is just to get information. They **do not** modify the data or the system.

1. **Release of Message Content:** Reading a private email or file.
2. **Traffic Analysis:** Observing the pattern of communication (who is talking to whom and how often).

* **Why they are dangerous:** They are very hard to detect because the system continues to work normally.

### B. Active Attacks (The "Troublemaker") 🔨

The attacker actively changes the data or affects the system operation.

1. **Masquerade:** Pretending to be someone else (Identity theft). 👤
2. **Replay:** Capturing a valid data unit and re-sending it later (e.g., re-sending a "Transfer $100" request). 🔄
3. **Modification of Messages:** Changing the content of the data. ✏️
4. **Denial of Service (DoS):** Overloading a server so it crashes and becomes unavailable. 🚫

### Comparison Table for Exams

| Feature | Passive Attack | Active Attack |
| --- | --- | --- |
| **Goal** | To obtain information. | To modify data or harm the system. |
| **Detection** | Very difficult. | Relatively easy. |
| **Focus** | Focus is on **Prevention** (Encryption). | Focus is on **Detection & Recovery**. |
| **System Impact** | No harm to system resources. | Harmful to system resources. |

---

## 📝 Summary & Revision Points

* **Security** is needed to protect the **CIA Triad** (Confidentiality, Integrity, Availability).
* **Approaches** include Trusted Systems, Perimeters, and the Layered (Onion) approach.
* **Attacks** are either **Passive** (stealing info silently) or **Active** (changing info or crashing systems).

### ⚠️ Common Mistakes to Avoid

* **Confusing Privacy with Confidentiality:** While related, in exams, use the term **Confidentiality** as it is the technical standard.
* **Ignoring Non-Repudiation:** Most students forget this 5th principle. Mentioning it earns extra marks!
* **Thinking Passive Attacks are "Better":** They are actually scarier because you don't know you've been hacked!

---
