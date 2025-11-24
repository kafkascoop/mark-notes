
---

# 🤖 Unit 1: Supervised Learning & Basic Methods

# Part 1

## Supervised Learning: Regression vs. Classification

### Introduction
Supervised Learning is the most fundamental paradigm in Machine Learning. It involves learning a mapping function from input variables ($\mathbf{X}$) to an output variable ($\mathbf{Y}$) based on a labeled dataset (data points where the 'correct answer' is already known). Think of it like a student studying from a textbook with **answers provided** in the back.

### Core Concepts and Definitions
* **Definition:** Given a set of input-output pairs $(x_i, y_i)$, the goal is to learn a function $f: \mathbf{X} \rightarrow \mathbf{Y}$ that can predict the output ($\hat{y}$) for a new input ($\hat{x}$).
* **Training Phase:** The model is "trained" using the labeled data.
* **Inference/Prediction Phase:** The trained model is used to predict outputs for unseen data.
* **The Two Types:** The nature of the output variable ($\mathbf{Y}$) defines the type of supervised learning:

| Feature | Regression 📉 | Classification 🏷️ |
| :--- | :--- | :--- |
| **Output Type (Y)** | **Continuous or Real-valued** (e.g., $5.2, 1000, -3.14$) | **Discrete/Categorical** (e.g., 'Yes/No', 'Dog/Cat/Bird', 'A/B/C') |
| **Goal** | Predict an **exact quantity** (e.g., price, temperature, age). | Predict a **class label** (e.g., spam or not spam, disease presence). |
| **Example Algorithms** | Linear Regression, Polynomial Regression, SVR. | Logistic Regression, Decision Trees, SVM, k-NN. |
| **Evaluation Metrics** | Mean Squared Error (MSE), $R^2$, Mean Absolute Error (MAE). | Accuracy, Precision, Recall, F1-Score, Confusion Matrix. |

### Diagram / Flowchart


### Real-life Examples or Analogies
| Type | Real-life Scenario | Input ($\mathbf{X}$) | Output ($\mathbf{Y}$) |
| :--- | :--- | :--- | :--- |
| **Regression** | **House Price Prediction** | Area, Location, \# of bedrooms | **Price in $\$$ (e.g., 500,000)** |
| **Classification** | **Email Filtering** | Words in email, Sender, Links | **'Spam' or 'Not Spam'** |

### Important Formulas / Keywords
* **Keywords:** Labeled Data, Training Set, Test Set, Feature ($\mathbf{X}$), Target ($\mathbf{Y}$), Hypothesis Function ($h(\mathbf{X})$).
* **Error Minimization (General Concept):** Supervised learning models try to minimize an **Error/Loss Function** (e.g., $J(\theta)$) between the predicted output $(\hat{y})$ and the actual output $(y)$.

### Tips to Memorize
* **Mnemonic:** **S**uper **L**earning is about **R**eally **C**alculating: **R**egression (Continuous $\rightarrow$ **R**eal Numbers) and **C**lassification (Discrete $\rightarrow$ **C**ategories).
* **Logic Trick:** If you have to **write a number with decimals** as the answer, it's **Regression**. If you have to **choose a label** from a fixed set, it's **Classification**.

---

## Distance-based Methods: Nearest-Neighbours (k-NN)

### Introduction
Distance-based methods use the concept of **similarity** or **proximity** between data points to make a prediction. The core assumption is that data points close to each other in the feature space are likely to belong to the same class or have similar target values. **k-Nearest Neighbours (k-NN)** is the most prominent and simplest example.

### Core Concepts and Definitions
* **k-NN Algorithm:** A **non-parametric**, **lazy learning** algorithm used for both **classification** and **regression**.
    * **Non-Parametric:** It makes no explicit assumptions about the functional form of $f(\mathbf{X})$ (e.g., linear, polynomial).
    * **Lazy Learning:** The model does not learn a discriminative function from the training data; all computation is deferred until prediction time. It simply *stores* the training dataset.
* **The 'k' Parameter:** This is the number of nearest neighbours considered. It is a **hyperparameter** chosen by the user.
    * **k-NN Classification:** The new data point is assigned the **majority class** of its $k$ nearest neighbours.
    * **k-NN Regression:** The new data point is assigned the **average** (or weighted average) of the target values of its $k$ nearest neighbours.
* **Distance Metric:** This determines how 'near' is measured. The most common is the **Euclidean Distance**.

### Diagram / Flowchart
**k-NN Classification Example (k=3):**
1.  Calculate the distance from the new point (star) to *all* training points.
2.  Select the $k=3$ nearest neighbours.
3.  Tally the classes of these $k$ neighbours (e.g., 2 Triangles, 1 Square).
4.  Assign the new point the majority class: Triangle.


### Real-life Examples or Analogies
* **Analogy (Social Networking):** Predicting if a new person (new data point) will like a certain product. You look at the $k$ closest friends (nearest neighbours) of that person who have rated the product. If most of them liked it (majority class), you predict the new person will like it too.
* **Medical Diagnosis:** A doctor assesses a new patient's symptoms (features) and looks up the records of the 5 most similar patients (k=5) they have treated to determine the most probable diagnosis.

### Important Formulas / Keywords
* **Keywords:** Lazy Learner, Non-parametric, Hyperparameter $k$, Euclidean Distance, Majority Vote (Classification).
* **Euclidean Distance (between two points $A$ and $B$ in $n$ dimensions):**
    $$d(A, B) = \sqrt{\sum_{i=1}^{n} (a_i - b_i)^2}$$

### Tips to Memorize & Common Mistakes
* **Mnemonic (k-NN steps):** **D**o **S**ome **C**alculations (**D**istance, **S**elect k-neighbours, **C**lassify/Regress).
* **Choosing 'k':** Smaller $k$ (e.g., $k=1$) leads to a **highly flexible model** (high variance, prone to **overfitting**). Larger $k$ leads to a **smoother model** (high bias, prone to **underfitting**). A common practice is to choose an **odd $k$** (like $k=3$ or $k=5$) to prevent ties in binary classification.
* **Common Mistake:** Forgetting to **normalize/standardize** the data. Since k-NN is distance-based, features with larger scales (e.g., 'Salary' in \$100k) will dominate the distance calculation over features with smaller scales (e.g., 'Age' in years). **Data scaling is crucial!**

---
---

## 💡 Summary and Revision Points

| Concept | Key Takeaway for 10 Marks | Exam Tip: Focus on... |
| :--- | :--- | :--- |
| **Supervised Learning** | Learns $f: \mathbf{X} \rightarrow \mathbf{Y}$ from **labeled data**. Divided into Classification (discrete $\mathbf{Y}$) and Regression (continuous $\mathbf{Y}$). | Differentiating the two types using **output type** and **evaluation metrics**. |
| **k-Nearest Neighbours** | A **lazy, non-parametric** method. Classification uses **majority vote**, Regression uses **average**. Requires a distance metric (Euclidean). | The dual characteristics (lazy/non-parametric), the role of $k$, and the necessity of **data scaling**. |

---
---
# Part2


# 🌳 Decision Trees

### Introduction
A Decision Tree (DT) is a **non-parametric supervised learning algorithm** that can be used for both **classification** and **regression**. It works by recursively partitioning the data space into smaller, distinct regions, resulting in a tree-like structure where internal nodes represent tests on features, branches represent the outcome of the test, and leaf nodes represent the final decision or prediction.

### Core Concepts and Definitions
* **Tree Structure:**
    * **Root Node:** Represents the entire dataset. The first split happens here.
    * **Internal Node:** Represents a feature test/condition (e.g., "Is Age $> 30$?").
    * **Branch/Edge:** Represents the outcome of the test (e.g., "Yes" or "No").
    * **Leaf Node (Terminal Node):** Represents the final class label (for classification) or a numerical value (for regression).
* **Splitting Criteria:** The core task is to find the "best" feature and threshold to split a node. This is done by maximizing the **homogeneity** (purity) of the resulting child nodes. Common metrics:
    * **Classification:** **Gini Impurity** or **Information Gain (using Entropy)**. We choose the split that results in the lowest Gini impurity or the highest Information Gain.
    * **Regression:** Reduction in **Variance** or **Mean Squared Error (MSE)**.
* **Stopping Criteria:** The recursive splitting stops when:
    * All data points in a node belong to the same class (pure node).
    * A maximum predefined depth is reached.
    * The number of data points in a node falls below a threshold.
* **Pruning:** The process of removing branches that make the tree overly complex (reducing **overfitting**). Pruning can be **pre-pruning** (stopping early) or **post-pruning** (building a full tree then cutting back).

### Important Formulas / Keywords
* **Keywords:** Gini Impurity, Entropy, Information Gain, Recursive Partitioning, Root Node, Leaf Node, Overfitting, Pruning.
* **Entropy (Measure of Impurity/Randomness):**
    $$H(S) = - \sum_{i=1}^{c} p_i \log_2(p_i)$$
    Where $p_i$ is the proportion of samples belonging to class $i$ in the set $S$. A pure node has $H(S)=0$.
* **Information Gain (Measure of Purity Improvement):**
    $$IG(S, A) = H(S) - \sum_{v \in Values(A)} \frac{|S_v|}{|S|} H(S_v)$$
    Where $S$ is the parent set, $A$ is the feature being split, and $S_v$ are the subsets resulting from the split. We select the feature $A$ that **maximizes $IG$**.

### Real-life Examples or Analogies
* **Flowchart Analogy:** A Decision Tree is literally a **"Choose Your Own Adventure"** book or a diagnostic flowchart a doctor follows:
    * *Start at Root: Patient has symptoms.*
    * *Test (Node): Is Temperature $> 100^\circ$F?*
        * *Yes (Branch): Go to Node X.*
        * *No (Branch): Go to Node Y.*
    * *Final Decision (Leaf): Prescribe Antibiotics.*

### Tips to Memorize & Common Mistakes
* **Logic Trick:** The best split is one that moves you **closer to zero impurity/entropy** or achieves the **highest Information Gain**. Think of **$IG$** as the "payoff" for making that specific split.
* **Common Mistake (Overfitting):** DTs are highly prone to overfitting, especially when allowed to grow too deep (creating many tiny, complex branches). **Always mention Pruning** as a remedy in your exam answer.
* **Exam Focus:** Be prepared to define Gini Impurity and Entropy, and briefly explain **why** we use Information Gain (to greedily select the best feature).

---
---

# 📜 Naive Bayes (NB)

### Introduction
Naive Bayes is a family of **probabilistic classifiers** based on applying **Bayes' Theorem** with a "naive" independence assumption between the features. It is a simple yet powerful algorithm, often used for text classification and real-time predictions due to its computational efficiency.

### Core Concepts and Definitions
* **Probabilistic Model:** NB calculates the probability of a data point belonging to a certain class ($C_k$) given its observed features ($\mathbf{x}$), i.e., $P(C_k | \mathbf{x})$.
* **Bayes' Theorem (Foundation):**
    $$P(C_k | \mathbf{x}) = \frac{P(\mathbf{x} | C_k) \cdot P(C_k)}{P(\mathbf{x})}$$
    * $P(C_k | \mathbf{x})$: **Posterior Probability** (What we want to find).
    * $P(\mathbf{x} | C_k)$: **Likelihood** (Probability of observing features $\mathbf{x}$ given the class $C_k$).
    * $P(C_k)$: **Prior Probability** (Probability of class $C_k$ occurring independently).
    * $P(\mathbf{x})$: **Evidence** (A normalizing constant; often ignored since we only compare numerators).
* **The "Naive" Assumption (Feature Independence):**
    * The core simplification is that **all features are independent of each other** given the class.
    * For a feature vector $\mathbf{x} = (x_1, x_2, \dots, x_n)$, the Likelihood calculation simplifies dramatically:
        $$P(\mathbf{x} | C_k) \approx P(x_1 | C_k) \cdot P(x_2 | C_k) \cdot \ldots \cdot P(x_n | C_k)$$
    * This assumption is rarely true in real life (e.g., in an email, 'Viagra' and 'cheap' are *not* independent words), but NB often performs surprisingly well despite this violation.

* **Prediction Rule (Maximum A Posteriori - MAP):**
    The classifier assigns the class $\hat{C}$ that has the highest posterior probability:
    $$\hat{C} = \arg\max_{C_k} P(C_k) \prod_{i=1}^{n} P(x_i | C_k)$$

### Important Formulas / Keywords
* **Keywords:** Bayes' Theorem, Prior, Posterior, Likelihood, Feature Independence, MAP (Maximum A Posteriori).
* **Laplace Smoothing (Additive Smoothing):** Used to prevent the **zero-frequency problem**. If a feature value is not present in the training data for a certain class, $P(x_i | C_k)$ becomes 0, which makes the entire product (posterior) 0. Smoothing adds a small constant (often 1) to the count of every feature to avoid this.

### Real-life Examples or Analogies
* **Spam Filtering:** This is the classic example. An email is classified as 'Spam' or 'Not Spam'.
    * **Prior:** $P(\text{Spam})$ (overall probability of an email being spam).
    * **Features:** The words in the email ($\mathbf{x}$).
    * **Likelihood:** $P(\text{word} | \text{Spam})$ (how often a word like "money" appears in spam emails).
* **Medical Analogy:** Predicting if a patient has a flu ($C_k$). You observe symptoms ($\mathbf{x}$). NB calculates the probability of the flu given the presence of a cough *and* a fever, treating the cough and fever as independent occurrences.

### Tips to Memorize & Common Mistakes
* **Mnemonic (NB Core):** **N**aive **B**ayes **I**s **P**robabilistic: **I**ndependence assumption, **P**osterior probability calculation.
* **Exam Focus:** Always define the **Naive Independence Assumption**—it's the core of the algorithm and the reason it's "Naive." Mention **Laplace Smoothing** as a critical practical requirement.
* **Advantages (for exam):** Simple, fast training/prediction, works well with high-dimensional data (like text).
* **Disadvantage (for exam):** Assumption of independence is often violated.

---
---

## 🧠 Mind Map / Revision Points

| Topic | Core Principle | Mechanism/Split Criterion | Key Challenge & Remedy |
| :--- | :--- | :--- | :--- |
| **Decision Trees** | Divide the feature space recursively to isolate pure classes/values. | Maximize **Information Gain** (using Entropy) or Minimize **Gini Impurity**. | **Overfitting** $\rightarrow$ Use **Pruning** (pre or post). |
| **Naive Bayes** | Apply Bayes' Theorem to find the highest **Posterior** probability. | **Likelihood** is calculated by multiplying individual feature probabilities (due to the **Naive Independence Assumption**). | **Zero-Frequency Problem** $\rightarrow$ Use **Laplace Smoothing**. |

---
---
 # Part 3
# 📐 Linear Models: Regression and Classification

## Linear Regression (LR)

### Introduction
**Linear Regression (LR)** is a foundational **Supervised Learning (Regression)** algorithm used to model the linear relationship between a continuous dependent variable (the target $\mathbf{Y}$) and one or more independent variables (the features $\mathbf{X}$). The underlying assumption is that the relationship between $\mathbf{X}$ and $\mathbf{Y}$ can be best described by a straight line or a hyperplane.

### Core Concepts and Definitions
* **Goal:** To find the optimal set of **weights** (coefficients, $\theta$) that minimize the difference between the predicted output $(\hat{y})$ and the actual output $(y)$.
* **Model Equation (Hypothesis Function):**
    * **Simple Linear Regression (One feature):**
        $$\hat{y} = \theta_0 + \theta_1 x_1$$
        Where $\theta_0$ is the **intercept** and $\theta_1$ is the **slope**.
    * **Multiple Linear Regression (n features):**
        $$\hat{y} = \theta_0 + \theta_1 x_1 + \theta_2 x_2 + \ldots + \theta_n x_n$$
        In vector form: $\mathbf{\hat{y}} = \mathbf{\theta}^T \mathbf{x}$
* **Cost Function (Loss Function):** The function used to measure the performance of the model. For LR, the standard is the **Mean Squared Error (MSE)** or **Sum of Squared Errors (SSE)**, which penalizes larger errors more heavily.
    $$MSE = \frac{1}{m} \sum_{i=1}^{m} (\hat{y}_i - y_i)^2$$
* **Optimization:** The model finds the optimal weights ($\mathbf{\theta}$) that minimize the MSE. This is typically achieved using **Gradient Descent** (iterative optimization) or the **Normal Equation** (analytical solution).

### Diagrams / Flowcharts
* **Concept:** A plot showing scattered data points and the best-fit straight line passing through them, minimizing the vertical distance (residual/error) to all points.
* **Optimization Flow:** (Start) Random $\mathbf{\theta}$ $\rightarrow$ (Loop) Calculate MSE $\rightarrow$ Calculate Gradient $\rightarrow$ Update $\mathbf{\theta}$ $\rightarrow$ (Stop) $\mathbf{\theta}$ Converges.

### Real-life Examples or Analogies
* **Salary vs. Experience:** Predicting a person's **salary (Y)** based on their **years of experience (X)**, assuming salary increases linearly with experience.
* **Predicting Rainfall:** Estimating the **amount of rainfall (Y)** based on atmospheric pressure, temperature, and humidity (multiple $\mathbf{X}$ features).

### Important Formulas / Keywords
* **Keywords:** Hypothesis Function, Weights ($\mathbf{\theta}$), Intercept, Slope, Mean Squared Error (MSE), Residuals, Gradient Descent, Normal Equation, Ordinary Least Squares (OLS).
* **Gradient Descent:** An optimization algorithm used to iteratively adjust the weights in the direction of the steepest descent of the cost function until a minimum is reached.
* **Assumptions of LR (Common Exam Question):**
    1.  **Linearity:** The relationship between $\mathbf{X}$ and $\mathbf{Y}$ is linear.
    2.  **Normality:** Residuals are normally distributed.
    3.  **Homoscedasticity:** The variance of the residuals is constant across all levels of $\mathbf{X}$.
    4.  **No Multicollinearity:** Independent variables are not highly correlated with each other.

### Common Mistakes to Avoid & Tips
* **Mistake:** Using LR when the relationship is clearly **nonlinear** (e.g., exponential growth).
* **Remedy:** Use **Polynomial Regression** (which is still a linear model in the weights) or non-linear models.
* **Mnemonic (LR Goal):** **L**inear **R**egression **M**ust **S**quare **E**rrors (**MSE**).

---
---

## Logistic Regression (LogR)

### Introduction
**Logistic Regression (LogR)** is a fundamental **Supervised Learning (Classification)** algorithm, despite having "Regression" in its name. It is used for predicting a **binary** (two-class) outcome, often modeled as the probability of a specific class or event occurring. It is a type of **Generalized Linear Model (GLM)**.

### Core Concepts and Definitions
* **Goal:** To estimate the **probability** $P(\mathbf{Y}=1 | \mathbf{X})$ that an input $\mathbf{X}$ belongs to the positive class (often labeled as '1').
* **The Sigmoid Function (Logistic Function):** LogR uses the standard linear equation ($\mathbf{\theta}^T \mathbf{x}$), but it feeds the result into a **Sigmoid** (or Logistic) function. This function squashes any input value (from $-\infty$ to $+\infty$) into a probability value between **0 and 1**.
    $$\sigma(z) = \frac{1}{1 + e^{-z}}$$
    Where $z = \mathbf{\theta}^T \mathbf{x}$.
* **Model Equation (Output):**
    $$\hat{P}(\mathbf{Y}=1 | \mathbf{X}) = \frac{1}{1 + e^{-(\mathbf{\theta}^T \mathbf{x})}}$$
* **Decision Boundary:** The model classifies the input based on the calculated probability:
    * If $\hat{P} \geq 0.5$, predict Class 1.
    * If $\hat{P} < 0.5$, predict Class 0.
    The point where $\hat{P}=0.5$ (i.e., $\mathbf{\theta}^T \mathbf{x} = 0$) defines the **linear decision boundary**.
* **Cost Function:** LR cannot use MSE because the Sigmoid function makes the cost function **non-convex**, resulting in many local minima that hinder Gradient Descent. LogR uses the **Log-Loss** (or **Binary Cross-Entropy**) function, which is convex and guarantees finding a unique global minimum.

### Diagrams / Flowcharts

* **Interpretation:** The Sigmoid curve visually represents how the linear combination of inputs is mapped onto a probability range. The steep S-shape shows that small changes in $z$ near 0 can lead to large changes in probability.

### Real-life Examples or Analogies
* **Credit Card Fraud Detection:** Predicting the probability (0 to 1) that a transaction is **fraudulent (1)** or **legitimate (0)**.
* **Customer Churn:** Predicting the probability that a customer will **leave (1)** or **stay (0)** based on their usage history.

### Important Formulas / Keywords
* **Keywords:** Binary Classification, Probability, Sigmoid Function, Log-Loss (Cross-Entropy), Odds Ratio, Decision Boundary, Generalized Linear Model (GLM).
* **Odds Ratio:** LogR can be interpreted in terms of odds. The term $\mathbf{\theta}^T \mathbf{x}$ is the **log-odds** (log of the ratio of the probability of success to the probability of failure).

### Tips to Memorize & Common Mistakes
* **Logic Trick:** Remember that LogR's job is to take the output of a standard **linear model** and force it into the **(0, 1) probability range** using the **Sigmoid function**.
* **Key Distinction (LR vs. LogR):**
    * LR predicts a **value** (continuous).
    * LogR predicts a **probability** (for a class label).
* **Common Mistake:** Confusing the term "regression" in Logistic Regression. Highlight in your answer that it is a **classification** algorithm.
* **Exam Focus:** Explain *why* the Sigmoid function is necessary (to convert linear output to probability) and *why* Cross-Entropy is used instead of MSE (to ensure a convex cost function).

---

## 📝 Comparative Table: Linear vs. Logistic Regression

| Feature | Linear Regression (LR) | Logistic Regression (LogR) |
| :--- | :--- | :--- |
| **Problem Type** | Regression | Classification (Binary, Multi-class) |
| **Output $\mathbf{Y}$** | Continuous Real Values | Probability (0 to 1) $\rightarrow$ Discrete Class Label |
| **Output Function** | Identity Function: $\hat{y} = \mathbf{\theta}^T \mathbf{x}$ | **Sigmoid Function:** $\hat{P} = \sigma(\mathbf{\theta}^T \mathbf{x})$ |
| **Cost Function** | Mean Squared Error (MSE) | Log-Loss / Binary Cross-Entropy |
| **Nature** | A standard linear model. | A **Generalized Linear Model (GLM)**. |

---
---

# Part 4

# 📈 Generalized Linear Models (GLMs)

### Introduction
**Generalized Linear Models (GLMs)** provide a unified framework that encompasses Linear Regression and Logistic Regression, extending the linear modeling approach to cases where the target variable ($\mathbf{Y}$) does not follow a normal distribution, but instead follows other distributions like Poisson, Bernoulli, or Gamma.

### Core Concepts and Definitions
* **The Three Components of a GLM:** Every GLM is defined by these three components:
    1.  **Random Component:** Specifies the **Probability Distribution** of the target variable $\mathbf{Y}$. This distribution belongs to the **Exponential Family** (e.g., Gaussian/Normal for continuous data, Bernoulli for binary data, Poisson for count data).
    2.  **Systematic Component:** The **Linear Predictor** ($\eta$). This is the standard linear combination of the features and weights:
        $$\eta = \theta_0 + \theta_1 x_1 + \ldots + \theta_n x_n = \mathbf{\theta}^T \mathbf{x}$$
    3.  **Link Function ($g(\cdot)$):** A function that connects the **expected mean ($\mu$)** of the random component to the **linear predictor ($\eta$)**.
        $$\eta = g(\mu) \quad \text{or equivalently} \quad \mu = g^{-1}(\eta)$$
        The link function ensures that the linear combination can be mapped appropriately to the scale of the mean.

### GLM Examples
| Model Type | Distribution ($\mathbf{Y}$) | Link Function ($g(\cdot)$) | Used For |
| :--- | :--- | :--- | :--- |
| **Linear Regression** | Gaussian (Normal) | **Identity Link:** $g(\mu) = \mu$ | Continuous target prediction |
| **Logistic Regression** | Bernoulli (Binomial) | **Logit Link:** $g(\mu) = \log(\frac{\mu}{1-\mu})$ | Binary classification (0/1) |
| **Poisson Regression** | Poisson | **Log Link:** $g(\mu) = \log(\mu)$ | Count data (e.g., number of events) |

### Real-life Examples or Analogies
* **Analogy:** A GLM is like a **universal adapter**. The linear predictor is the same core "plug" (the linear combination). The **Link Function** is the adapter that lets the plug fit into different "sockets" (the different distributions of the target variable).
* **Poisson Regression Example:** Predicting the **number of emergency room visits (counts)** per day based on weather and pollution levels. Since the output must be a non-negative integer (a count), the Poisson distribution is appropriate, requiring a Log Link function.

### Important Formulas / Keywords
* **Keywords:** Exponential Family, Link Function, Linear Predictor ($\eta$), Expected Mean ($\mu$), Identity Link, Logit Link, Poisson.

### Tips to Memorize & Common Mistakes
* **Mnemonic (GLM Components):** **L**earn **R**eally **S**mart: **L**ink, **R**andom, **S**ystematic.
* **Common Mistake:** Thinking all GLMs are linear regression. Clarify that while they all use a **linear combination of features**, the **relationship between the mean and the predictor** is not always linear (it's non-linear if the link function is non-identity, e.g., Sigmoid for LogR).

---

# 🛡️ Support Vector Machines (SVM)

### Introduction
**Support Vector Machines (SVM)** are powerful, non-probabilistic linear or non-linear supervised algorithms primarily used for **classification** (though they can be adapted for regression, SVR). The core principle is to find the **best possible separating boundary** (a hyperplane) that maximizes the **margin** between the closest points of different classes.

### Core Concepts and Definitions
* **Hyperplane:** The decision boundary in an $n$-dimensional space (a line in 2D, a plane in 3D). The SVM goal is to find the equation of this optimal hyperplane.
* **Support Vectors (SVs):** The training data points that are closest to the optimal hyperplane. These points **support** the hyperplane and are critical; if they are moved, the hyperplane changes. All other points are irrelevant to the final model boundary.
* **Margin:** The distance between the hyperplane and the nearest Support Vector from either class. SVM aims to **maximize this margin** (Maximum Margin Classifier). A wider margin generally leads to better generalization on unseen data.
* **Soft Margin vs. Hard Margin:**
    * **Hard Margin:** Strictly requires all training data to be perfectly separable by the hyperplane. (Highly sensitive to outliers, prone to overfitting).
    * **Soft Margin:** Allows for some misclassification or margin violation (controlled by the hyperparameter **C**). This is more robust and commonly used in practice.
* **Kernel Trick (for Non-linearity):** When data is not linearly separable in the original input space, the **Kernel Trick** is used.
    * It implicitly maps the data into a **higher-dimensional feature space** where the data *becomes* linearly separable, without actually calculating the coordinates in that high-dimensional space.
    * Common Kernels: **Polynomial, Radial Basis Function (RBF)**, Sigmoid.

### Diagram / Flowcharts


### Real-life Examples or Analogies
* **Separating Walls:** Imagine trying to build a wall (hyperplane) to separate two groups of children (classes) playing in a field (data space). The best wall isn't one that just barely separates them, but one that is **equidistant from the two closest children** in each group (Support Vectors), providing the maximum safety buffer (margin).
* **Facial Recognition:** SVMs excel in classification tasks like identifying faces or hand-written characters where separating complex, non-linear data is necessary.

### Important Formulas / Keywords
* **Keywords:** Hyperplane, Support Vectors (SVs), Margin, Hard Margin, Soft Margin (C parameter), **Kernel Trick**, Radial Basis Function (RBF), Maximum Margin Classifier.
* **Objective:** The optimization problem for SVM involves minimizing $\frac{1}{2} ||\mathbf{w}||^2$ (to maximize the margin, since margin is $2/||\mathbf{w}||$), subject to the constraint that all points are correctly classified (or only mildly misclassified in the soft-margin case).

### Tips to Memorize & Common Mistakes
* **Logic Trick:** The power of SVM comes from the **Support Vectors** and the **Kernel Trick**. If the question mentions non-linear data or high-dimensional separation, immediately think of the **RBF Kernel**.
* **Exam Focus:** Define SVM as a **maximum margin classifier** and provide a detailed explanation of the **Kernel Trick** (mapping to higher dimension, implicitly).

---

# 🧩 Beyond Binary Classification

This final section covers advanced supervised learning concepts that extend the techniques learned above.

### A. Multi-class Classification
Many real-world problems involve classifying data into more than two classes (e.g., classifying images into 'Dog', 'Cat', 'Bird').

* **Methods to Adapt Binary Classifiers (like SVM or LogR):**
    1.  **One-vs-Rest (OvR) / One-vs-All (OvA):**
        * Train $K$ separate binary classifiers (where $K$ is the number of classes).
        * Classifier $k$ is trained to distinguish Class $k$ from **all other** $K-1$ classes.
        * **Prediction:** The new data point is assigned the class whose classifier outputs the highest score.
        * *Advantage:* Simple to implement.
    2.  **One-vs-One (OvO) / Pairwise:**
        * Train a binary classifier for **every distinct pair** of classes.
        * Requires training $\frac{K(K-1)}{2}$ classifiers.
        * **Prediction:** Uses a "voting" scheme. The class that wins the most pairwise contests is the final prediction.
        * *Advantage:* Suitable for algorithms like SVM, which scale poorly with large $K$.

### B. Structured Output Prediction
* **Concept:** Predicting an output that is not a single category or value, but an **interconnected structure** (e.g., a sequence, a tree, or a graph). The components of the output are dependent on each other.
* **Example:** **Part-of-Speech Tagging** (NLP). Given a sentence, predicting the grammatical tag (Noun, Verb, Adjective, etc.) for *each word*. The tag for the current word depends on the tag of the previous word.
* **Algorithms:** Conditional Random Fields (CRFs), Recurrent Neural Networks (RNNs).

### C. Ranking
* **Concept:** The goal is not just to classify or predict a value, but to learn an ordering or **preference list** of items based on a query.
* **Example:** **Search Engine Results.** Given a user's search query, the model ranks the documents based on relevance, not just classifying them as relevant/irrelevant.
* **Techniques:** **Learning to Rank (LTR)** methods, often using algorithms like RankSVM.

---
---

## 🎉 Final Unit 1 Revision Checklist

| Topic Covered | Keywords to Define | Must Mention |
| :--- | :--- | :--- |
| **GLMs** | Random/Systematic Component, Link Function, Exponential Family | The three components and the **purpose of the link function** (connecting mean to linear predictor). |
| **SVM** | Hyperplane, Support Vectors, Margin, **Kernel Trick** | **Maximize the Margin**; the **RBF kernel** for non-linear separation. |
| **Beyond Binary** | OvR, OvO, Structured Output, Ranking | **OvR/OvO** strategies for multi-class; **Interdependence** of output elements in structured prediction. |



