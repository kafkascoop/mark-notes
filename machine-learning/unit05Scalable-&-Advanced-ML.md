
---

# 🌐 Unit 5: Scalable and Advanced ML Topics

## 1. Scalable Machine Learning

### Introduction
As data volumes grow into the terabyte and petabyte range, traditional in-memory training methods become infeasible. **Scalable ML** focuses on techniques to train models efficiently using vast datasets by processing data incrementally or distributing computation across multiple machines.

### 1.1. Online Learning (Incremental Learning)
* **Concept:** The model updates its parameters **sequentially** as new data arrives (data stream). It processes one or a small batch of data points at a time, instead of the entire dataset.
* **Mechanism:** Uses optimization methods like **Stochastic Gradient Descent (SGD)**, which computes the gradient and updates the weights based on a single sample or a small mini-batch.
* **Advantages:**
    * **Scalability:** Can handle datasets too large to fit in memory (out-of-core learning).
    * **Adaptability:** Ideal for systems where the underlying data distribution changes over time (**concept drift**), as the model continuously adapts.
* **Disadvantages:** Sensitive to the order of the training examples.
* **Keywords:** Data Stream, **SGD**, Mini-Batch, Concept Drift, Out-of-Core.

### 1.2. Distributed Learning
* **Concept:** Breaking down the training workload and distributing it across a cluster of multiple computing nodes (machines) to achieve faster training times.
* **Mechanism:**
    * **Data Parallelism:** The most common approach. The model architecture is identical on all nodes, but each node trains on a different, non-overlapping subset of the data. The gradients from all nodes are then aggregated to update the global model parameters.
    * **Model Parallelism:** The model itself is too large to fit on one machine, so different layers or components of the model are split across different nodes.
* **Challenges:** Network communication overhead for syncing gradients and weights is often the bottleneck.
* **Keywords:** Cluster Computing, **Data Parallelism**, Model Parallelism, Parameter Server, Gradient Synchronization.

---

## 2. Advanced Learning Paradigms

### 2.1. Semi-supervised Learning (SSL) 🏷️
* **Concept:** Utilizes a large amount of **unlabeled data** alongside a small amount of **labeled data** for training.
* **Goal:** To leverage the structure/distribution knowledge contained in the cheap unlabeled data to improve the performance achieved by only using the expensive labeled data.
* **Assumption:** Data points close to each other should share the same label (smoothness assumption).
* **Techniques:** **Self-training** (use the labeled set to train a model, then use that model to label the unlabeled data, and retrain).
* **Keywords:** Labeled + Unlabeled Data, Self-training, Smoothness Assumption.

### 2.2. Active Learning ❓
* **Concept:** The learning algorithm itself **selects** the most informative, unlabelled data points and asks an oracle (usually a human expert) to label them.
* **Goal:** To achieve high accuracy using as **few labels as possible**, minimizing labeling costs.
* **Strategy:** The model typically queries data points near the current decision boundary (where it is most uncertain) or those that are most representative of the data distribution.
* **Keywords:** Query Strategy, Informative Samples, Uncertainty Sampling, Cost Reduction.

### 2.3. Reinforcement Learning (RL) 🎮
* **Concept:** Training an **Agent** to interact with an **Environment** by performing **Actions** to maximize a cumulative **Reward**. The agent learns through trial and error, not labeled examples.
* **Key Components:**
    * **Agent:** The learning program.
    * **Environment:** The external world.
    * **State ($S$):** Current situation of the environment.
    * **Action ($A$):** Move made by the agent.
    * **Reward ($R$):** Immediate feedback after an action.
    * **Policy ($\pi$):** A mapping from states to actions ($\pi: S \rightarrow A$). This is what the agent learns.
* **Goal:** Find the optimal Policy ($\pi^*$) that maximizes the **Expected Future Discounted Reward**.
* **Keywords:** Agent, Environment, Policy, **Reward Maximization**, Trial and Error, Q-Learning.

---

## 3. Bayesian Learning and Graphical Models

### 3.1. Introduction to Bayesian Learning and Inference
* **Concept:** A philosophical approach where probability is used to represent the degree of belief (epistemic uncertainty) in a hypothesis. Learning involves updating prior beliefs with observed evidence.
* **Bayes' Theorem (Foundation):**
    $$P(H | D) = \frac{P(D | H) \cdot P(H)}{P(D)}$$
    * $P(H)$: **Prior Belief** (Initial belief in hypothesis $H$).
    * $P(D | H)$: **Likelihood** (How well the hypothesis explains the observed data $D$).
    * $P(H | D)$: **Posterior Belief** (Updated belief in $H$ after seeing $D$).
* **Inference:** Using the posterior distribution to make predictions or decisions.
* **Advantages:** Provides a measure of uncertainty (the posterior distribution) and naturally incorporates prior domain knowledge.
* **Keywords:** **Prior**, **Likelihood**, **Posterior**, Degree of Belief, Uncertainty.

### 3.2. Inference in Graphical Models
* **Concept:** A **Probabilistic Graphical Model (PGM)** uses a graph structure to represent the probabilistic relationships (dependencies/conditional independencies) between a set of random variables.
* **Types:**
    * **Bayesian Networks (Directed Acyclic Graphs - DAGs):** Represents **causal relationships**.
    * **Markov Random Fields (Undirected Graphs):** Represents mutual influence/correlation.
* **Inference Goal:** To compute the marginal or conditional probability distributions of variables, typically by summing out (integrating over) unobserved variables.
* **Examples of Inference:** Calculating the probability of a disease (unobserved) given a set of observed symptoms.
* **Keywords:** **PGM**, Bayesian Network (DAG), Markov Random Field, Conditional Independence, Marginalization.

---

## 💡 Unit 5 Revision Checklist

| Topic | Core Concept | Key Technique | Contrast/Application |
| :--- | :--- | :--- | :--- |
| **Online Learning** | Updates model sequentially, out-of-core. | **Stochastic Gradient Descent (SGD)** | Use for streaming data or concept drift. |
| **Distributed Learning**| Distribute computation across multiple nodes. | **Data Parallelism** (syncing gradients) | Use for massive static datasets (Terabytes+). |
| **Semi-supervised** | Uses small labeled + large unlabeled data. | Self-training | Bridges supervised and unsupervised learning. |
| **Active Learning** | Model selects the most informative data to label. | Uncertainty Sampling | Focus on minimizing labeling costs. |
| **Reinforcement** | Agent learns policy to maximize reward. | **Policy**, **Q-Learning** | No labeled data; learns via trial and error. |
| **Bayesian Learning** | Updates belief (prior) with evidence. | **Bayes' Theorem** (Prior $\rightarrow$ Posterior) | Provides a full uncertainty distribution. |