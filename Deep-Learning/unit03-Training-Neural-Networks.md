## 3. Unit 3: Training Neural Networks

### 3.1. Risk Minimization and Loss Function

This section defines the goal of training: translating the learning problem into a quantifiable mathematical objective.

#### Introduction

Training a neural network is essentially an optimization problem. The primary goal is **Risk Minimization**, which means finding the set of network parameters (weights and biases) that minimizes the discrepancy between the network's predictions and the true target values across the training data.

#### Core Concepts and Definitions

* **Empirical Risk Minimization (ERM)** 📉:
    * Since the true underlying data distribution (the true **risk**) is unknown, we approximate it by minimizing the **Empirical Risk** (or **Average Loss**) calculated over the finite training dataset.
    * **Goal:** Find the parameters $\boldsymbol{W}^*$ that minimize the average loss $L$ over all $N$ training examples $(\boldsymbol{x}_i, y_i)$:
        $$\boldsymbol{W}^* = \arg \min_{\boldsymbol{W}} \frac{1}{N} \sum_{i=1}^{N} L(f(\boldsymbol{x}_i; \boldsymbol{W}), y_i)$$
    * Here, $f(\boldsymbol{x}_i; \boldsymbol{W})$ is the network's prediction and $L$ is the **Loss Function**.

* **Loss Function (Cost Function or Objective Function)** 🎯:
    * A function that quantifies the penalty for an incorrect prediction. It measures how "bad" the model's prediction is compared to the true value for a **single data point**.
    * The choice of loss function depends entirely on the type of learning problem:

| Problem Type | Standard Loss Function | Formula / Purpose |
| :--- | :--- | :--- |
| **Regression** (Predicting continuous values) | **Mean Squared Error (MSE)** | $L(\hat{y}, y) = (\hat{y} - y)^2$. Calculates the squared difference between predicted ($\hat{y}$) and true ($y$) values. |
| **Binary Classification** (Two classes) | **Binary Cross-Entropy (BCE)** | $L = - [y \log(\hat{y}) + (1-y) \log(1-\hat{y})]$. Penalizes predictions based on how far they are from the true probability. |
| **Multi-Class Classification** (More than two classes) | **Categorical Cross-Entropy (CCE)** | Measures the difference between the true probability distribution (one-hot encoded $y$) and the predicted distribution ($\hat{y}$). |

#### Real-life Analogy

Think of a marksman aiming at a target.
* **True Risk:** The marksman's inherent inaccuracy due to wind, fatigue, etc. (Unknown and unchangeable).
* **Empirical Risk:** The average distance of all the shots fired so far from the bullseye.
* **Loss Function:** The score given for a single shot based on how far it landed from the center. The marksman adjusts their aim (the parameters $\boldsymbol{W}$) to minimize the average score (ERM).

#### Tips to Memorize

* **Risk vs. Loss:** **Loss** is for a **Single** data point; **Risk** is the **Average Loss** across the dataset.
* **Cross-Entropy:** Used for classification because it acts like a measure of "surprise" or difference between distributions.

#### Common Mistakes to Avoid

* Using **MSE** for classification. While technically possible, it penalizes "confidence" too much and is less effective than **Cross-Entropy** in driving probability-based models.

---

### 3.2. Backpropagation (BP)

Backpropagation is the core algorithm used to efficiently calculate the gradients needed to train a neural network.

#### Introduction

The goal of training is to adjust the weights $\boldsymbol{W}$ to minimize the loss $L$. This adjustment is done by calculating the **gradient** $\frac{\partial L}{\partial \boldsymbol{W}}$, which tells us the direction and magnitude of the steepest ascent in the loss landscape. **Backpropagation** is an application of the **chain rule** of calculus that calculates these gradients layer-by-layer, moving backward from the output.

#### Core Concepts and Definitions

* **Chain Rule** ⛓️: The mathematical foundation. To find the derivative of a composite function, you multiply the derivatives of the individual functions. In a neural network, the loss is a composite function of all the weights.
    $$\frac{dy}{dx} = \frac{dy}{dz} \cdot \frac{dz}{dx}$$

* **The Two Passes** 🚶:
    1.  **Forward Pass:** Input data $\boldsymbol{x}$ travels through the network, layer-by-layer, computing activations and the final prediction $\hat{y}$. The loss $L$ is calculated.
    2.  **Backward Pass (Backpropagation):** The error gradient $\frac{\partial L}{\partial a^{(l)}}$ is calculated at the output layer and then passed **backward** to compute the gradient for the weights $\frac{\partial L}{\partial W^{(l)}}$ at each layer $l$. This is done iteratively from the last hidden layer to the first.

* **Weight Update Rule** 🛠️: Once the gradient is known, the weights are updated using an optimizer (like SGD):
    $$\boldsymbol{W}_{\text{new}} = \boldsymbol{W}_{\text{old}} - \eta \cdot \frac{\partial L}{\partial \boldsymbol{W}}$$
    * $\eta$ (eta) is the **learning rate**, controlling the step size.



#### Step-by-Step Flow (Backward Pass)

1.  **Output Layer Gradient:** Calculate the error derivative with respect to the output neuron's input $z_{\text{out}}$. This is often $\frac{\partial L}{\partial \hat{y}} \cdot \frac{\partial \hat{y}}{\partial z_{\text{out}}}$.
2.  **Propagate Back:** Use the chain rule to calculate the gradient $\frac{\partial L}{\partial z^{(l)}}$ for the previous layer $l$. This gradient depends on the gradients of all neurons in the subsequent layer $l+1$.
3.  **Calculate Weight Gradients:** Use the propagated gradient to compute $\frac{\partial L}{\partial W^{(l)}}$ and $\frac{\partial L}{\partial b^{(l)}}$ for the current layer.
4.  **Repeat:** Continue propagating the error backward until the first hidden layer is reached.

#### Real-life Analogy

Imagine a pipeline manufacturing process where the final product is flawed (the loss).
* **Forward Pass:** The data (raw materials) going through the pipeline (layers).
* **Loss:** The inspection revealing the final flaw.
* **Backpropagation:** Tracing the flaw **backward** through each station (layer) to find out which machine (weight) contributed most to the error, allowing for precise adjustments at the source.

#### Tips to Memorize

* **BP Key Idea:** Calculates the **partial derivative** of the loss with respect to **every parameter**.
* **Chain Rule:** The mathematical trick that makes BP efficient by reusing calculations.

#### Common Mistakes to Avoid

* Not understanding that BP is *just* the efficient method for calculating gradients, not the optimization algorithm itself (that's **Gradient Descent**).
* Confusing the role of the activation function's derivative, which is essential for determining how much a neuron's input contributed to the error.

---

### 3.3. Regularization and Model Selection

This topic addresses methods used to combat overfitting and the process of choosing the best model configuration.

#### Introduction

Neural networks often have millions of parameters, making them highly susceptible to **overfitting**—where the model learns the training data and its noise too well, performing poorly on unseen test data. **Regularization** techniques are implemented to constrain the model's complexity and improve its generalization ability. **Model Selection** is the process of choosing the optimal architecture and hyperparameters.

#### Core Concepts: Regularization ⚖️

Regularization modifies the loss function or the network structure to prevent weights from becoming too large or too dependent on specific features.

1.  **L2 Regularization (Weight Decay)**:
    * Adds the square of the weights to the loss function.
        $$L_{\text{total}} = L_{\text{original}} + \lambda \sum_{\boldsymbol{W}} \boldsymbol{W}^2$$
    * **Effect:** Encourages smaller, more dispersed weights, preventing any single weight from dominating the learning.

2.  **L1 Regularization**:
    * Adds the absolute value of the weights to the loss function.
    * **Effect:** Tends to drive irrelevant weights completely to zero, promoting **sparsity** (feature selection).

3.  **Dropout** 🚪:
    * During training, randomly **drops out** (sets to zero) a percentage of neurons and their connections in the hidden layers.
    * **Effect:** Prevents complex co-adaptations between neurons, forcing the network to learn more **robust** and redundant representations, as no single neuron can rely solely on another.

4.  **Early Stopping** 🛑:
    * Monitors the performance of the model on a separate **validation set** during training.
    * **Procedure:** Stop training when the validation loss starts to *increase* (indicating overfitting), even though the training loss might still be decreasing.

#### Core Concepts: Model Selection

This involves choosing the best **hyperparameters** (settings *before* training) and architecture.

1.  **Hyperparameters** ⚙️: Parameters not learned by the algorithm itself, including:
    * Learning Rate ($\eta$)
    * Number of Hidden Layers and Neurons
    * Regularization Strength ($\lambda$)
    * Batch Size

2.  **Data Split** 🔪: For robust model selection:
    * **Training Set:** Used to train the network parameters (weights/biases). (e.g., 70-80%)
    * **Validation Set:** Used for **hyperparameter tuning** and **early stopping**. The model *never* trains on this data. (e.g., 10-15%)
    * **Test Set:** Used only **once** at the very end to give an unbiased estimate of the final model's generalization ability. (e.g., 10-15%)

3.  **Cross-Validation (k-Fold CV)**: A technique where the training data is divided into $k$ folds. The model is trained $k$ times, each time using a different fold as the validation set, providing a more robust estimate of performance.

#### Important Formulas / Keywords

* **Keywords:** **Overfitting**, **Generalization**, **Weight Decay**, **Sparsity**, **Dropout**, **Validation Set**, **Hyperparameter**, **Test Set**.

#### Tips to Memorize

* **L2/L1** penalize **large weights**.
* **Dropout** penalizes **co-dependence** among neurons.
* **Validation set** is your **tuner**, **Test set** is your **final grade**.

#### Common Mistakes to Avoid

* Tuning hyperparameters based on the **Test Set** performance. This "leaks" information and makes the test set result an overly optimistic measure of performance.
* Applying dropout at the output layer (usually not done).

---

### 3.4. Optimization

Optimization algorithms are essential to efficiently navigate the high-dimensional loss landscape and find the set of weights that minimizes the loss.

#### Introduction

The goal of optimization is to iteratively update the network weights and biases using the gradients calculated by backpropagation to find the **minimum** of the loss function.

#### Core Concepts and Definitions

1.  **Stochastic Gradient Descent (SGD)** 🐌:
    * Updates the weights using the gradient calculated from just **one randomly chosen example** (or a very small batch) at a time.
    * **Pro:** Very fast updates; avoids getting stuck in sharp local minima.
    * **Con:** High variance in updates; "noisy" path toward the minimum.

2.  **Batch Gradient Descent (BGD)**:
    * Updates the weights using the gradient calculated from the **entire training dataset**.
    * **Pro:** Smooth, direct path to the minimum; guaranteed convergence.
    * **Con:** Very slow for large datasets; can get stuck in sharp local minima.

3.  **Mini-Batch Gradient Descent** (The Standard) ⚡:
    * Updates the weights using the gradient calculated from a small, randomly selected **batch** of data (e.g., 32, 64, 128 examples).
    * **Pro:** Combines the stability of BGD with the speed of SGD; the industry standard.

4.  **Advanced Optimizers (Adaptive Learning Rate)** 🚀:
    * These modern methods (like **Adam**, RMSProp, Adagrad) adapt the learning rate $\eta$ for each parameter individually based on the history of its past gradients.
    * **Adam (Adaptive Moment Estimation):** The most popular choice. It combines the advantages of **Momentum** (helping the optimizer roll past shallow local minima) and **RMSProp** (adjusting learning rates based on how frequently a parameter's gradient changes).

#### Diagram: Optimization Landscape



#### Important Formulas / Keywords

* **Keywords:** **Gradient Descent**, **SGD**, **BGD**, **Mini-Batch**, **Learning Rate ($\eta$ )**, **Local Minimum**, **Momentum**, **Adam**.
* **Weight Update (General):** $\boldsymbol{W}_{\text{new}} = \boldsymbol{W}_{\text{old}} - \text{Optimizer\_Update}(\frac{\partial L}{\partial \boldsymbol{W}})$

#### Tips to Memorize

* **SGD** vs. **Mini-Batch**: Always use **Mini-Batch** unless the problem is very small.
* **ADAM** is usually the best **starting point** optimizer for most deep learning problems.

#### Common Mistakes to Avoid

* Using a **learning rate** that is too **high** will cause the optimization to **overshoot** the minimum and potentially diverge.
* Using a learning rate that is too **low** will cause the training to take an **extremely long time** to converge.

