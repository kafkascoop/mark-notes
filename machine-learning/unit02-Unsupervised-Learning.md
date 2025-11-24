
# 👻 Unit 2: Unsupervised Learning

## 1. Unsupervised Learning Overview

### Introduction
**Unsupervised Learning** deals with training a model on datasets that are **unlabeled**, meaning the data only contains input features ($\mathbf{X}$) with no corresponding output variable or "correct answer" ($\mathbf{Y}$). The model's job is to infer the intrinsic structure, patterns, or groupings within the data. Think of it like a student trying to understand a concept without a solution key.

### Core Concepts and Definitions
* **Goal:** To learn the underlying distribution, structure, or representation of the data.
* **Key Tasks:**
    1.  **Clustering:** Grouping similar data points together (e.g., K-means).
    2.  **Dimensionality Reduction:** Reducing the number of features while retaining maximum information (e.g., PCA).
    3.  **Density Estimation:** Estimating the probability distribution of the data.
* **Contrast with Supervised Learning:**
    | Feature | Unsupervised Learning | Supervised Learning |
    | :--- | :--- | :--- |
    | **Data** | Unlabeled Data ($\mathbf{X}$ only) | Labeled Data ($\mathbf{X}$ and $\mathbf{Y}$) |
    | **Goal** | Find hidden patterns/structure | Predict known output $\mathbf{Y}$ |
    | **Feedback** | No external feedback (uses internal metrics) | Uses error/loss function ($\hat{y}$ vs $y$) |

### Real-life Examples
* **Market Segmentation:** Grouping customers into distinct segments based on their purchasing behavior.
* **Anomaly Detection:** Identifying rare events or outliers (e.g., unusual network traffic).

---

## 2. Clustering: K-means and Kernel K-means

### Introduction
**Clustering** is the task of partitioning the dataset into groups, called **clusters**, such that data points within the same cluster are more similar to each other than to those in other clusters. **K-means** is the most popular, simple, and effective partition-based clustering algorithm.

---

### 2.1. K-means Clustering

#### Core Concepts and Definitions
* **Algorithm Type:** Partitioning (divides data into non-overlapping subgroups).
* **The 'K' Parameter:** The number of clusters to form. It is a **hyperparameter** chosen beforehand.
* **Centroid:** The center point (mean vector) of all data points belonging to a specific cluster.
* **Mechanism (Iterative Refinement):**
    1.  **Initialization:** Choose $K$ initial centroid locations (often randomly).
    2.  **Assignment Step:** Assign every data point to the cluster whose centroid is the **closest** (based on Euclidean distance).
    3.  **Update Step:** Recalculate the position of each cluster's centroid as the **mean** of all points assigned to that cluster.
    4.  **Repeat:** Steps 2 and 3 until the centroids no longer move significantly (i.e., convergence).

#### Important Formulas / Keywords
* **Keywords:** Centroid, Euclidean Distance, Iterative Refinement, Convergence, Within-Cluster Sum of Squares (WCSS).
* **Objective Function (Inertia/WCSS):** K-means attempts to minimize the sum of squared distances between each point and its assigned centroid:
    $$J = \sum_{j=1}^{K} \sum_{i \in S_j} ||x_i - \mu_j||^2$$
    Where $\mu_j$ is the centroid of cluster $S_j$.

#### Tips to Memorize & Common Mistakes
* **Logic Trick:** K-means is a "mean" algorithm; it relies on calculating the average (mean) position to define the cluster center.
* **Common Mistakes:**
    1.  **Sensitive to Initial Centroids:** Different starting points can lead to different final clusterings (local minima). Use methods like **K-means++** for smart initialization.
    2.  **Sensitive to Scale:** Like k-NN, K-means uses distance, so **data scaling (normalization)** is crucial.
    3.  **Assumes Spherical Clusters:** It performs poorly on non-spherical or oddly shaped clusters.

---

### 2.2. Kernel K-means

#### Core Concepts and Definitions
* **Challenge:** Standard K-means works poorly when data clusters are **non-linearly separable** (non-spherical or interwoven).
* **Solution:** **Kernel K-means** addresses this by implicitly mapping the data into a **higher-dimensional feature space** (similar to the SVM Kernel Trick) where the clusters might become linearly (or spherically) separable.
* **Mechanism:** Instead of using the standard Euclidean distance in the original space, it uses a **kernel function** (like the RBF kernel) to compute a measure of similarity in the high-dimensional space. The entire K-means algorithm is then reformulated using kernel functions, avoiding explicit coordinate mapping.

#### Keywords
* **Keywords:** Non-linear Clustering, Kernel Function, Feature Space Mapping, RBF Kernel.

---

## 3. Dimensionality Reduction: PCA and Kernel PCA

### Introduction
**Dimensionality Reduction** (DR) is the process of reducing the number of random variables (features) under consideration by obtaining a set of **principal features**. The primary goal is to combat the "Curse of Dimensionality," speed up training, and visualize high-dimensional data, all while preserving the most important variance.

---

### 3.1. Principal Component Analysis (PCA)

#### Core Concepts and Definitions
* **Algorithm Type:** **Linear** DR technique that relies on maximizing variance.
* **Goal:** To find a new set of orthogonal axes (called **Principal Components - PCs**) that capture the maximum variance in the original data. The first PC captures the most variance, the second PC the second most, and so on.
* **Mechanism (Eigen-decomposition):**
    1.  **Standardize** the data.
    2.  Calculate the **Covariance Matrix** of the data.
    3.  Compute the **Eigenvectors** and **Eigenvalues** of the covariance matrix.
    4.  The **Eigenvectors** are the new **Principal Components** (the directions).
    5.  The **Eigenvalues** represent the **variance** captured by each PC.
    6.  Select the top $k$ eigenvectors (based on the largest eigenvalues) to form the final $k$-dimensional subspace.
* **Property:** PCA is an **orthogonal linear transformation**.

#### Important Formulas / Keywords
* **Keywords:** Variance Maximization, Principal Component (PC), Orthogonal Transformation, Covariance Matrix, Eigenvector, Eigenvalue, Scree Plot.

#### Common Mistakes to Avoid & Tips
* **Mistake:** Forgetting to **standardize** the data. If features are on different scales, PCA will simply maximize the variance of the feature with the largest scale, regardless of its importance.
* **Mnemonic (PCA Steps):** **S**tudy **C**ovariance **E**xtensively: **S**tandardize, **C**ovariance matrix, **E**igen-decomposition.

---

### 3.2. Kernel PCA

#### Core Concepts and Definitions
* **Challenge:** Standard PCA is **linear**. It fails to effectively reduce the dimensionality when the data distribution is non-linear (e.g., a Swiss roll shape).
* **Solution:** **Kernel PCA** (KPCA) first implicitly maps the data into a high-dimensional feature space using a **kernel function** (like RBF) and then applies standard PCA in that feature space.
* **Result:** It can find **non-linear principal components**, allowing for effective DR even when the data has complex underlying manifold structures.

#### Keywords
* **Keywords:** Non-linear Dimensionality Reduction, Kernel Trick, Non-linear Manifold.

---

## 4. Matrix Factorization and Matrix Completion

### Introduction
These techniques decompose a large data matrix into two or more smaller matrices. This is primarily used for finding **latent factors** (hidden patterns) and for handling missing data.

### Core Concepts and Definitions
* **Matrix Factorization (MF):** Decomposing a large matrix $\mathbf{R}$ into the product of two matrices, $\mathbf{P}$ and $\mathbf{Q}$, such that $\mathbf{R} \approx \mathbf{P} \cdot \mathbf{Q}^T$.
    * $\mathbf{R}$: The original data matrix (e.g., Users $\times$ Items rating matrix).
    * $\mathbf{P}$: Latent factor matrix for Users.
    * $\mathbf{Q}$: Latent factor matrix for Items.
    * **Goal:** The columns of $\mathbf{P}$ and $\mathbf{Q}$ represent the **latent features** (e.g., movie genres, user interests) that explain the observed data.
* **Matrix Completion:** A direct application of MF, specifically aiming to predict the **missing entries** in the original matrix $\mathbf{R}$ using the decomposed matrices $\mathbf{P}$ and $\mathbf{Q}$.

### Real-life Examples
* **Recommender Systems (Netflix Prize):** Predicting a user's rating for a movie they haven't seen yet (filling in a missing entry) by factoring the large User-Movie rating matrix.

---

## 5. Generative Models

### Introduction
**Generative Models** are models that learn the full probability distribution of the data, $P(\mathbf{X})$. Unlike discriminative models (which learn $P(\mathbf{Y}|\mathbf{X})$ for prediction), generative models aim to understand how the data was generated, allowing them to **generate new, synthetic data** similar to the training data.

### Core Concepts and Definitions
#### 5.1. Mixture Models (e.g., Gaussian Mixture Models - GMM)
* **Concept:** Assumes that the entire dataset was generated by a mixture of a small number of underlying probability distributions (e.g., several Gaussian distributions).
* **Gaussian Mixture Models (GMM):** Assumes the data comes from $K$ different multivariate Gaussian distributions. It is an extension of K-means that provides a **probabilistic clustering** (each point has a probability of belonging to each cluster).
* **Training:** Uses the **Expectation-Maximization (EM) algorithm** to iteratively estimate the parameters (mean, variance, and weight) of each Gaussian component.

#### 5.2. Latent Factor Models
* **Concept:** Assumes that the observed data is generated from a set of **unobserved, underlying variables** called **latent factors** (or hidden variables).
* **Example:** In image processing, the observed pixels are generated by latent factors like 'object presence', 'lighting', and 'texture'.
* **Examples:** Latent Dirichlet Allocation (LDA) for topic modeling, and, conceptually, Matrix Factorization (where $\mathbf{P}$ and $\mathbf{Q}$ are latent factor matrices).

### Keywords
* **Keywords:** Generative vs. Discriminative, $P(\mathbf{X})$, Expectation-Maximization (EM), Gaussian Component, Latent Variable/Factor.

---

## 💡 Unit 2 Revision Checklist

| Topic | Core Principle | Mechanism/Key Term | Primary Weakness |
| :--- | :--- | :--- | :--- |
| **K-means** | Partition data into $K$ spherical clusters. | Centroid, WCSS Minimization | Sensitive to initialization and non-spherical clusters. |
| **PCA** | Linearly reduce dimensionality by maximizing variance. | Eigenvectors/Eigenvalues, Covariance Matrix | Only captures **linear** relationships (non-linear data is difficult). |
| **Kernel PCA** | PCA applied in a higher-dimensional space. | Kernel Trick, Non-linear DR | Computationally intensive. |
| **Matrix Factorization** | Decompose $\mathbf{R}$ into $\mathbf{P} \cdot \mathbf{Q}^T$. | Latent Factors, Matrix Completion | Scalability and cold-start problems (new users/items). |
| **Generative Models** | Learn the entire distribution $P(\mathbf{X})$. | EM Algorithm, Latent Factors | More complex to train than discriminative models. |
