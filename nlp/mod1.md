## 📘 NLP Study Notes: Module 1 (Foundational NLP)

**Level:** Undergraduate Engineering (Final Year)

**Goal:** Comprehensive 10-Mark Answer Prep 🎓

---

## 1. Introduction to NLP & Regular Expressions

Natural Language Processing (NLP) is the intersection of Computer Science, Linguistics, and AI. Its primary goal is to map "Natural Language" into a representation that a computer can process.

### A. Regular Expressions (Regex) 🔍

Regex is the algebraic notation for characterizing text sequences. In NLP, it is the first step in **Tokenization** and **Information Extraction**.

* **Disjunction:** `[wW]oodchuck` matches "woodchuck" or "Woodchuck".
* **Ranges:** `[A-Z]` matches any uppercase letter.
* **Kleene Plus (+):** 1 or more occurrences.
* **Kleene Star (*):** 0 or more occurrences.
* **Anchors:** `^` (start of line), `$` (end of line).

### B. Finite State Automata (FSA) ⚙️

An FSA is a mathematical model consisting of states and transitions.

* **DFA (Deterministic):** From any state, there is exactly one transition for a given input symbol.
* **NFA (Non-Deterministic):** There can be multiple transitions or even transitions on empty strings ().

> **Exam Tip:** If asked to design an FSA for "sheep" (baaaaaa!), show the start state, the sequence of 'a' transitions, and the final "double-circle" state.

---

## 2. Tokenization, Normalization, and NER ✂️

### A. Word Tokenization & Segmentation

The process of breaking a stream of text into **Tokens** (words, numbers, or symbols).

* **Challenges:** * **Contractions:** "don't"  "do" + "not".
* **Punctuation:** "Ph.D." should be one token, but "end." should be "end" + ".".


* **Sentence Segmentation:** Identifying boundaries using cues like `?`, `!`, and `.`.

### B. Named Entity Recognition (NER) 🏷️

Identifying "Proper Nouns" and classifying them into pre-defined categories.

* **IOB Tagging:** * **B-PER:** Beginning of Person name.
* **I-PER:** Inside of Person name.
* **O:** Outside any entity.


* **Example:** `[B-PER Steve] [I-PER Jobs] [O founded] [B-ORG Apple]`.

---

## 3. Spell Checking: The Bayesian Approach 🧠

This is a high-weightage topic for 10-mark questions. It uses the **Noisy Channel Model**.

### Core Theory:

We assume the user meant to type word  (correct), but it went through a "noisy channel" and came out as  (wrong). We want to find:


Using Bayes' Theorem:



*Since  is constant for all candidates, we ignore the denominator.*

### The Two Components:

1. **Prior Probability  (Language Model):** How frequent is the word "apple" in English? Calculated from a large corpus.
2. **Likelihood  (Error Model/Channel Model):** What is the probability that  was mistyped as ? This uses a **Confusion Matrix** (Insertion, Deletion, Substitution, Transposition).

---

## 4. Minimum Edit Distance (MED) 📏

MED is the minimum number of editing operations (Insertion, Deletion, Substitution) required to transform string  into .

### Dynamic Programming Approach:

We use a matrix  where the value represents the distance between  and .

* **Deletion Cost:** 1
* **Insertion Cost:** 1
* **Substitution Cost:** 2 (called **Levenshtein Distance**) or 1.

**Formula:**


---

## 5. Morphology & Finite State Transducers (FST) 🧩

### A. Inflectional vs. Derivational Morphology

* **Inflectional:** Adds grammatical information (tense, number). Word class remains the same (e.g., *cat*  *cats*).
* **Derivational:** Creates new words, often changing the word class (e.g., *happy* (Adj)  *happiness* (Noun)).

### B. Morphological Parsing with FST

A Morphological Parser takes a word like **"foxes"** and returns:
`fox + N + PL` (Noun, Plural).

**The FST (Finite State Transducer):**
An FST is like an FSA but has two tapes: **Input Tape** and **Output Tape**.

* It performs a mapping between the **Lexical Level** (abstract morphemes) and the **Surface Level** (actual spelling).

### C. Orthographic Rules (Spelling Rules)

FSTs can also handle spelling changes.

* **Example:** The "e-insertion" rule. *fox* + *s*  *foxes* (not *foxs*). This is handled by cascading FSTs.

---

## 6. Porter Stemmer 🪵

The Porter Stemmer is a list of rules (heuristics) applied in 5 sequential steps to strip suffixes.

* **Step 1a:** `SSES`  `SS` (e.g., *caresses*  *caress*).
* **Step 1b:** `ING`   (if there is a vowel in the stem).
* **Limitation:** It is a "crude" chopper. It doesn't know context. (e.g., *organization*  *organ*).

---

## 🚀 Revision Summary Table

| Topic | Key Tool | Main Goal |
| --- | --- | --- |
| **Regex** | Pattern Strings | Finding text patterns. |
| **FSA** | State Diagrams | Recognizing valid strings. |
| **MED** | Matrix/DP | Measuring string similarity. |
| **Bayesian** | Bayes' Rule | Probabilistic spell correction. |
| **FST** | 2-Tape Automata | Mapping surface form to lexical form. |
| **Stemming** | Heuristic Rules | Reducing words to their root/stem. |

### 💡 Tips to Memorize:

* **MED Calculation:** Always start your matrix at index `(0,0)` with value `0`. Fill row 0 and col 0 with increments of 1.
* **Bayes Formula:** Remember **"P-L-C"**: **P**rior  **L**ikelihood = **C**onclusion.
* **Morphology:** **I**nflectional = **I**dentical Category; **D**erivational = **D**ifferent Category.

**Common Exam Question:** "Explain the Lexicon and Morphotactics in Morphological Parsing."

* **Answer:** Lexicon is the list of stems/affixes. Morphotactics is the model (usually an FSA) that decides which classes of morphemes can follow others (e.g., you can't put a plural suffix before a stem).

---

