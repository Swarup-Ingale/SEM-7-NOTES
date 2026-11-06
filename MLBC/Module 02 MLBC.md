# Master Academic Study Guide: Mumbai University MLBC Module 02 Examination Answers

## Module 2: Supervised Learning Algorithms and Ensemble Methods

---

### Question 1 (10 Marks):
**(a) Detail the mathematical formulation of Multiple Linear Regression. Derive the analytical closed-form Normal Equation using Ordinary Least Squares (OLS).**  
**(b) Explain the Gradient Descent optimization algorithm. Contrast $L_1$ (Lasso) and $L_2$ (Ridge) regularization techniques with their geometric interpretations and cost function formulations.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Mathematical Formulation** | Linear hypothesis, feature matrix representation, and OLS Mean Squared Error (MSE) cost function equation. | **2 Marks** |
| **Normal Equation Derivation** | Matrix calculus derivation steps: expanding $J(\mathbf{w})$, computing gradient $\nabla_{\mathbf{w}} J(\mathbf{w})$, setting to zero, and solving for $\mathbf{w}$. | **3 Marks** |
| **Gradient Descent Algorithm** | Iterative update rule, learning rate $\alpha$, batch vs. mini-batch variants, and ASCII convergence flowchart. | **2.5 Marks** |
| **Regularization Analysis** | Formulas for Ridge ($L_2$) and Lasso ($L_1$), penalty terms, sparsity effects, and comparison table. | **2.5 Marks** |

---

#### 2. Part (a): Multiple Linear Regression & Normal Equation Derivation

##### Mathematical Formulation
Multiple Linear Regression models a continuous scalar target variable $y \in \mathbb{R}$ as a linear combination of $n$ input feature variables $\mathbf{x} = [x_1, x_2, \dots, x_n]^T \in \mathbb{R}^n$ parameterized by weight vector $\mathbf{w} = [w_1, w_2, \dots, w_n]^T$ and bias term $w_0$:

$$\hat{y} = w_0 + w_1 x_1 + w_2 x_2 + \dots + w_n x_n = w_0 + \sum_{j=1}^{n} w_j x_j$$

By defining a dummy intercept feature $x_0 = 1$, the expression simplifies into matrix vector dot product notation:

$$\hat{y} = \mathbf{w}^T \mathbf{x} \quad \text{where} \quad \mathbf{w} = \begin{bmatrix} w_0 \\ w_1 \\ \vdots \\ w_n \end{bmatrix} \in \mathbb{R}^{(n+1) \times 1}, \quad \mathbf{x} = \begin{bmatrix} 1 \\ x_1 \\ \vdots \\ x_n \end{bmatrix} \in \mathbb{R}^{(n+1) \times 1}$$

For a dataset containing $m$ independent training observations $\{( \mathbf{x}^{(1)}, y^{(1)} ), ( \mathbf{x}^{(2)}, y^{(2)} ), \dots, ( \mathbf{x}^{(m)}, y^{(m)} )\}$, the entire system of linear equations is compactly represented using the Design Matrix $\mathbf{X} \in \mathbb{R}^{m \times (n+1)}$ and target vector $\mathbf{y} \in \mathbb{R}^{m \times 1}$:

$$\mathbf{X} = \begin{bmatrix} 1 & x_1^{(1)} & x_2^{(1)} & \dots & x_n^{(1)} \\ 1 & x_1^{(2)} & x_2^{(2)} & \dots & x_n^{(2)} \\ \vdots & \vdots & \vdots & \ddots & \vdots \\ 1 & x_1^{(m)} & x_2^{(m)} & \dots & x_n^{(m)} \end{bmatrix}, \quad \mathbf{y} = \begin{bmatrix} y^{(1)} \\ y^{(2)} \\ \vdots \\ y^{(m)} \end{bmatrix}, \quad \hat{\mathbf{y}} = \mathbf{X} \mathbf{w}$$

##### Ordinary Least Squares (OLS) Cost Function
The Ordinary Least Squares framework minimizes the Mean Squared Error (MSE) cost function $J(\mathbf{w})$, measuring the squared residual differences between actual target values $\mathbf{y}$ and predicted values $\hat{\mathbf{y}}$:

$$J(\mathbf{w}) = \frac{1}{2m} \sum_{i=1}^{m} \left( \hat{y}^{(i)} - y^{(i)} \right)^2 = \frac{1}{2m} (\mathbf{X}\mathbf{w} - \mathbf{y})^T (\mathbf{X}\mathbf{w} - \mathbf{y})$$

##### Step-by-Step Derivation of the Closed-Form Normal Equation
To find the optimal parameter weight vector $\mathbf{w}^*$ that minimizes $J(\mathbf{w})$, we expand the matrix product and differentiate with respect to $\mathbf{w}$.

**Step 1: Matrix Expansion of the Cost Function**
$$J(\mathbf{w}) = \frac{1}{2m} \left( (\mathbf{X}\mathbf{w})^T - \mathbf{y}^T \right) (\mathbf{X}\mathbf{w} - \mathbf{y})$$
$$J(\mathbf{w}) = \frac{1}{2m} \left( \mathbf{w}^T \mathbf{X}^T \mathbf{X} \mathbf{w} - \mathbf{w}^T \mathbf{X}^T \mathbf{y} - \mathbf{y}^T \mathbf{X} \mathbf{w} + \mathbf{y}^T \mathbf{y} \right)$$

Since $\mathbf{w}^T \mathbf{X}^T \mathbf{y}$ is a $1 \times 1$ scalar value, its transpose equals itself:
$$(\mathbf{w}^T \mathbf{X}^T \mathbf{y})^T = \mathbf{y}^T \mathbf{X} \mathbf{w}$$

Combining the inner scalar terms yields:
$$J(\mathbf{w}) = \frac{1}{2m} \left( \mathbf{w}^T \mathbf{X}^T \mathbf{X} \mathbf{w} - 2 \mathbf{w}^T \mathbf{X}^T \mathbf{y} + \mathbf{y}^T \mathbf{y} \right)$$

**Step 2: Differentiating with respect to Weight Vector $\mathbf{w}$**
Applying matrix gradient rules ($\frac{\partial}{\partial \mathbf{w}} (\mathbf{w}^T \mathbf{A} \mathbf{w}) = 2 \mathbf{A} \mathbf{w}$ for symmetric matrix $\mathbf{A}$, and $\frac{\partial}{\partial \mathbf{w}} (\mathbf{w}^T \mathbf{b}) = \mathbf{b}$):

$$\nabla_{\mathbf{w}} J(\mathbf{w}) = \frac{\partial J(\mathbf{w})}{\partial \mathbf{w}} = \frac{1}{2m} \left( 2 \mathbf{X}^T \mathbf{X} \mathbf{w} - 2 \mathbf{X}^T \mathbf{y} \right) = \frac{1}{m} \left( \mathbf{X}^T \mathbf{X} \mathbf{w} - \mathbf{X}^T \mathbf{y} \right)$$

**Step 3: Setting Gradient to Zero and Solving for $\mathbf{w}$**
Setting the gradient vector equal to zero vector $\mathbf{0}$:

$$\frac{1}{m} \left( \mathbf{X}^T \mathbf{X} \mathbf{w} - \mathbf{X}^T \mathbf{y} \right) = \mathbf{0}$$
$$\mathbf{X}^T \mathbf{X} \mathbf{w} = \mathbf{X}^T \mathbf{y}$$

Multiplying both sides by the inverse matrix $(\mathbf{X}^T \mathbf{X})^{-1}$ (assuming $\mathbf{X}^T \mathbf{X}$ is non-singular and invertible):

$$\mathbf{w}^* = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$$

This closed-form solution yields the exact global minimum in $O(n^3)$ matrix inversion computation time.

---

#### 3. Part (b): Gradient Descent & Regularization Techniques

##### Gradient Descent Optimization
When feature count $n$ is very large ($n > 10,000$), calculating the matrix inverse $(\mathbf{X}^T \mathbf{X})^{-1}$ becomes computationally prohibitively expensive. Gradient Descent iteratively optimizes weight parameters by taking steps proportional to the negative gradient of the loss function:

$$\mathbf{w}^{(t+1)} := \mathbf{w}^{(t)} - \alpha \nabla_{\mathbf{w}} J(\mathbf{w}^{(t)})$$

Where $\alpha > 0$ represents the learning rate hyperparameter. Component-wise, for feature $j$:

$$w_j := w_j - \alpha \frac{1}{m} \sum_{i=1}^{m} \left( h_{\mathbf{w}}(\mathbf{x}^{(i)}) - y^{(i)} \right) x_j^{(i)}$$

##### ASCII Flowchart: Gradient Descent Optimization Loop
```
  [Start Training]
         │
         ▼
  [Initialize Weights w=0, Learning Rate α]
         │
         ▼
  ┌─────────────────────────────────────────┐
  │ Compute Predictions: y_hat = X * w      │
  │ Compute Loss: J(w) = (1/2m) ||y_hat-y||²│
  └─────────────────────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────────────┐
  │ Compute Gradient: ∇J = (1/m) X^T(y_hat-y)│
  └─────────────────────────────────────────┘
         │
         ▼
  ┌─────────────────────────────────────────┐
  │ Update Weights: w := w - α * ∇J         │
  └─────────────────────────────────────────┘
         │
  ───────┴───────────────────────────────
 │  Is Convergence Reached? ||∇J|| < ε   │
  ───────┬───────────────────────────────
         │ No                      │ Yes
         │                         ▼
         └──────────────► [Optimal Model Weights w*]
```

##### Regularized Regression Models: Ridge ($L_2$) vs. Lasso ($L_1$)
Regularization prevents model overfitting by adding a penalty term $R(\mathbf{w})$ to the MSE loss function, constraining weight magnitude:

$$J_{\text{regularized}}(\mathbf{w}) = \text{MSE}(\mathbf{w}) + \lambda R(\mathbf{w})$$

1. **Ridge Regression ($L_2$ Regularization):** Adds squared $L_2$-norm penalty $\sum_{j=1}^n w_j^2$:
   $$J_{\text{Ridge}}(\mathbf{w}) = \frac{1}{2m} \sum_{i=1}^{m} \left( \mathbf{w}^T \mathbf{x}^{(i)} - y^{(i)} \right)^2 + \frac{\lambda}{2m} \sum_{j=1}^{n} w_j^2$$
   *Closed-Form Solution:* $\mathbf{w}_{\text{Ridge}} = (\mathbf{X}^T \mathbf{X} + \lambda \mathbf{I})^{-1} \mathbf{X}^T \mathbf{y}$ (Guarantees invertibility even when $\mathbf{X}^T \mathbf{X}$ is singular).

2. **Lasso Regression ($L_1$ Regularization):** Adds absolute $L_1$-norm penalty $\sum_{j=1}^n |w_j|$:
   $$J_{\text{Lasso}}(\mathbf{w}) = \frac{1}{2m} \sum_{i=1}^{m} \left( \mathbf{w}^T \mathbf{x}^{(i)} - y^{(i)} \right)^2 + \frac{\lambda}{m} \sum_{j=1}^{n} |w_j|$$
   *Sparsity Property:* Due to sharp diamond-shaped geometric constraint contours at axes intersections, Lasso drives irrelevant feature weights *exactly to zero*, performing implicit automatic feature selection.

##### Structural Comparison Matrix: Regression & Regularization Paradigms

| Technical Attribute | Simple / Multiple Linear Regression | Ridge Regression ($L_2$) | Lasso Regression ($L_1$) | ElasticNet Regression |
| :--- | :--- | :--- | :--- | :--- |
| **Penalty Function** | None ($R(\mathbf{w}) = 0$) | $\lambda \sum_{j=1}^n w_j^2$ ($L_2$ norm) | $\lambda \sum_{j=1}^n \|w_j\|$ ($L_1$ norm) | $r \lambda \|w\|_1 + \frac{1-r}{2} \lambda \|w\|_2^2$ |
| **Closed-Form Solution** | $\mathbf{w} = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$ | $(\mathbf{X}^T \mathbf{X} + \lambda \mathbf{I})^{-1} \mathbf{X}^T \mathbf{y}$ | No closed form (Coordinate Descent) | No closed form (Iterative Optimization) |
| **Feature Sparsity** | No ($w_j \ne 0$) | No (shrinks weights toward zero) | **Yes** (drives non-informative $w_j \to 0$) | **Yes** (handles correlated feature groups) |
| **Primary Use Case** | Baseline unregularized modeling | High multicollinearity among features | Feature selection in high-dimensional data | Combined grouping + feature selection |

---

### Question 2 (10 Marks):
**(a) Explain Logistic Regression for Binary Classification. Derive the Binary Cross-Entropy loss function using Maximum Likelihood Estimation (MLE).**  
**(b) Detail the Naive Bayes Classifier framework based on Bayes' Theorem. Explain Gaussian, Multinomial, and Bernoulli Naive Bayes variants.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Logistic Regression Formulation** | Sigmoid transformation, log-odds hypothesis, and probabilistic decision boundary. | **2 Marks** |
| **MLE Loss Derivation** | Likelihood function $L(\mathbf{w})$, log-likelihood transformation, and Binary Cross-Entropy derivation. | **3 Marks** |
| **Naive Bayes Principle** | Bayes' Theorem, Conditional Independence assumption formulation, and posterior calculation steps. | **2.5 Marks** |
| **Naive Bayes Variants** | Gaussian NB (continuous data), Multinomial NB (word counts), Bernoulli NB (binary features), and comparison. | **2.5 Marks** |

---

#### 2. Part (a): Logistic Regression & Loss Function Derivation

##### Probabilistic Model Formulation
Logistic Regression addresses binary classification problems ($y \in \{0, 1\}$) by passing a linear combination of input features $z = \mathbf{w}^T \mathbf{x}$ through the non-linear Sigmoid (Logistic) activation function $\sigma(z)$:

$$p = P(y=1|\mathbf{x}; \mathbf{w}) = \sigma(\mathbf{w}^T \mathbf{x}) = \frac{1}{1 + e^{-\mathbf{w}^T \mathbf{x}}} = \frac{1}{1 + e^{-(w_0 + w_1 x_1 + \dots + w_n x_n)}}$$

##### Properties of the Sigmoid Activation Function
1. Bounded domain and range: Maps unbounded real values $(-\infty, +\infty)$ strictly into probabilistic range $(0, 1)$.
2. Symmetry and decision boundary: $\sigma(0) = 0.5$. If $\mathbf{w}^T \mathbf{x} \ge 0 \implies \hat{y} = 1$; if $\mathbf{w}^T \mathbf{x} < 0 \implies \hat{y} = 0$.
3. Analytical Derivative: $\frac{d\sigma(z)}{dz} = \sigma(z)(1 - \sigma(z))$.

##### Log-Odds Transformation
The ratio of positive probability to negative probability defines the Odds Ratio:

$$\frac{P(y=1|\mathbf{x})}{P(y=0|\mathbf{x})} = \frac{p}{1-p} = e^{\mathbf{w}^T \mathbf{x}}$$

Taking the natural logarithm yields the Logit (Log-Odds) transformation, proving that Logistic Regression models log-odds linearly:

$$\ln\left( \frac{p}{1-p} \right) = \mathbf{w}^T \mathbf{x} = w_0 + w_1 x_1 + \dots + w_n x_n$$

##### ASCII Diagram: Sigmoid Pipeline & Decision Boundary
```
  [Input Features x] ──► [Linear Combination: z = w^T x] ──► [Sigmoid: σ(z) = 1/(1+e^-z)] ──► Prob p ∈ (0,1)
                                                                                               │
                                                                 ┌─────────────────────────────┴┐
                                                                 ▼                              ▼
                                                           If p ≥ 0.5                     If p < 0.5
                                                                 │                              │
                                                                 ▼                              ▼
                                                          [Class Label 1]                [Class Label 0]
```

##### Step-by-Step Derivation of Binary Cross-Entropy Loss via Maximum Likelihood Estimation (MLE)

**Step 1: Formulating Individual Sample Probabilities**
For a target label $y^{(i)} \in \{0, 1\}$ and predicted probability $\hat{y}^{(i)} = \sigma(\mathbf{w}^T \mathbf{x}^{(i)})$:

$$P(y^{(i)}=1|\mathbf{x}^{(i)}) = \hat{y}^{(i)}$$
$$P(y^{(i)}=0|\mathbf{x}^{(i)}) = 1 - \hat{y}^{(i)}$$

Combining both conditional statements into a single Bernoulli distribution equation:

$$P(y^{(i)}|\mathbf{x}^{(i)}; \mathbf{w}) = \left( \hat{y}^{(i)} \right)^{y^{(i)}} \left( 1 - \hat{y}^{(i)} \right)^{1 - y^{(i)}}$$

**Step 2: Constructing the Likelihood Function**
Assuming $m$ training observations are independent and identically distributed (i.i.d.), the Likelihood Function $L(\mathbf{w})$ is the joint probability product:

$$L(\mathbf{w}) = \prod_{i=1}^{m} P(y^{(i)}|\mathbf{x}^{(i)}; \mathbf{w}) = \prod_{i=1}^{m} \left( \hat{y}^{(i)} \right)^{y^{(i)}} \left( 1 - \hat{y}^{(i)} \right)^{1 - y^{(i)}}$$

**Step 3: Transforming to Log-Likelihood Function**
Taking the natural logarithm $\ell(\mathbf{w}) = \ln L(\mathbf{w})$ converts products into summations:

$$\ell(\mathbf{w}) = \ln \left( \prod_{i=1}^{m} \left( \hat{y}^{(i)} \right)^{y^{(i)}} \left( 1 - \hat{y}^{(i)} \right)^{1 - y^{(i)}} \right)$$
$$\ell(\mathbf{w}) = \sum_{i=1}^{m} \left[ y^{(i)} \ln\left( \hat{y}^{(i)} \right) + (1 - y^{(i)}) \ln\left( 1 - \hat{y}^{(i)} \right) \right]$$

**Step 4: Defining Binary Cross-Entropy Cost Function**
In optimization, cost functions are minimized. Reversing sign and scaling by $\frac{1}{m}$ yields the Binary Cross-Entropy (Log Loss) cost function $J(\mathbf{w})$:

$$J(\mathbf{w}) = -\frac{1}{m} \ell(\mathbf{w}) = -\frac{1}{m} \sum_{i=1}^{m} \left[ y^{(i)} \ln\left( \hat{y}^{(i)} \right) + (1 - y^{(i)}) \ln\left( 1 - \hat{y}^{(i)} \right) \right]$$

---

#### 3. Part (b): Naive Bayes Classifier & Algorithmic Variants

##### Foundational Framework via Bayes' Theorem
The Naive Bayes classifier is a probabilistic supervised learning algorithm based on Bayes' Theorem:

$$P(y|\mathbf{x}) = \frac{P(\mathbf{x}|y) \cdot P(y)}{P(\mathbf{x})} = \frac{P(x_1, x_2, \dots, x_n | y) \cdot P(y)}{P(x_1, x_2, \dots, x_n)}$$

Where $P(y|\mathbf{x})$ is the Posterior Probability, $P(\mathbf{x}|y)$ is the Class Likelihood, $P(y)$ is the Class Prior Probability, and $P(\mathbf{x})$ is the Marginal Predictor Probability.

##### Naive Conditional Independence Assumption
Naive Bayes assumes that all feature attributes $x_1, x_2, \dots, x_n$ are conditionally independent given the class label $y$:

$$P(x_1, x_2, \dots, x_n | y) = P(x_1|y) \cdot P(x_2|y) \cdots P(x_n|y) = \prod_{j=1}^{n} P(x_j|y)$$

Substituting this assumption into Bayes' Theorem and omitting the constant marginal denominator $P(\mathbf{x})$ yields the decision rule:

$$\hat{y} = \arg\max_{y \in Y} P(y) \prod_{j=1}^{n} P(x_j|y)$$

##### Naive Bayes Variants

1. **Gaussian Naive Bayes:** Used when features contain continuous numerical values. Likelihood is modeled using a Normal (Gaussian) distribution:
   $$P(x_j|y) = \frac{1}{\sqrt{2\pi\sigma_{y,j}^2}} \exp\left( -\frac{(x_j - \mu_{y,j})^2}{2\sigma_{y,j}^2} \right)$$
   Where $\mu_{y,j}$ and $\sigma_{y,j}^2$ represent the class-specific mean and variance for feature $j$.

2. **Multinomial Naive Bayes:** Designed for discrete frequency counts (e.g., text document term frequencies). Feature likelihood uses multinomial distributions with Laplace Smoothing ($\alpha=1$):
   $$P(x_j|y) = \frac{N_{y,x_j} + \alpha}{N_y + \alpha n}$$

3. **Bernoulli Naive Bayes:** Applied when feature attributes are binary boolean indicators ($x_j \in \{0, 1\}$), evaluating rule occurrences:
   $$P(\mathbf{x}|y) = \prod_{j=1}^{n} \left[ P(i|y)^{x_j} (1 - P(i|y))^{(1 - x_j)} \right]$$

---

### Question 3 (10 Marks):
**(a) Detail Decision Tree construction via the CART algorithm. Mathematically define Gini Impurity, Shannon Entropy, and Information Gain.**  
**(b) Explain tree pruning techniques (Pre-pruning vs. Post-pruning) to resolve overfitting in Decision Trees.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Decision Tree Principles** | Recursive binary partitioning, CART framework, and tree node anatomy. | **2 Marks** |
| **Mathematical Impurity Metrics** | Exact formulas for Gini Index, Shannon Entropy, Information Gain, and Gain Ratio. | **3 Marks** |
| **CART vs. ID3 Comparison** | Comparative table covering split types, attribute types, and criteria. | **2.5 Marks** |
| **Tree Pruning & Regularization** | Pre-pruning stopping conditions, Post-pruning cost-complexity logic, and ASCII tree structure. | **2.5 Marks** |

---

#### 2. Part (a): CART Algorithm & Mathematical Impurity Metrics

##### Principles of Decision Tree Induction
Decision Tree algorithms construct hierarchical flow-chart structures by recursively splitting feature spaces into axis-aligned hyperplanes. The Classification and Regression Tree (CART) algorithm builds strict binary trees by evaluating candidate feature splits to maximize purity gain across child nodes.

##### Mathematical Definitions of Impurity Metrics

1. **Gini Impurity (Gini Index):** Measures the probability of a randomly chosen element being incorrectly labeled if it were randomly labeled according to the distribution of labels in the node dataset $D$:
   $$\text{Gini}(D) = 1 - \sum_{k=1}^{K} (p_k)^2$$
   Where $p_k$ is the proportion of elements in dataset $D$ belonging to class $k$ across $K$ classes.
   *   Pure node ($p_1 = 1, p_2 = 0 \implies \text{Gini} = 0$).
   *   Maximum impurity for binary classification ($p_1 = 0.5, p_2 = 0.5 \implies \text{Gini} = 0.5$).

   When candidate feature $A$ splits dataset $D$ into two binary child partitions $D_1$ and $D_2$:
   $$\text{Gini}_A(D) = \frac{|D_1|}{|D|} \text{Gini}(D_1) + \frac{|D_2|}{|D|} \text{Gini}(D_2)$$
   The split yielding the lowest weighted impurity $\text{Gini}_A(D)$ is selected.

2. **Shannon Entropy:** Quantifies the expected information content or uncertainty contained within dataset node $D$:
   $$\text{Entropy}(D) = -\sum_{k=1}^{K} p_k \log_2(p_k)$$
   *   Pure node ($\text{Entropy} = 0$).
   *   Maximum uncertainty binary split ($\text{Entropy} = 1.0$ bit).

3. **Information Gain:** Measures the net reduction in Entropy achieved by splitting dataset $D$ on feature attribute $A$:
   $$\text{Information Gain}(D, A) = \text{Entropy}(D) - \sum_{v \in \text{Values}(A)} \frac{|D_v|}{|D|} \text{Entropy}(D_v)$$

4. **Gain Ratio:** Mitigates Information Gain's inherent bias toward selecting high-cardinality attributes (e.g., unique primary keys) by normalizing with Split Information:
   $$\text{SplitInfo}_A(D) = -\sum_{v \in \text{Values}(A)} \frac{|D_v|}{|D|} \log_2\left( \frac{|D_v|}{|D|} \right)$$
   $$\text{Gain Ratio}(D, A) = \frac{\text{Information Gain}(D, A)}{\text{SplitInfo}_A(D)}$$

##### ASCII Architectural Diagram: Binary Decision Tree Splitting
```
                      [ Root Node: Dataset D (N=100) ]
                      [ Gini(D) = 0.50, Entropy = 1.0  ]
                                     │
                        Feature Split: x1 ≤ 4.5 ?
                         ┌───────────┴───────────┐
                      Yes│                       │No
                         ▼                       ▼
            [ Left Child Node D1 ]      [ Right Child Node D2 ]
            [ N1 = 60, Pure Class 0 ]   [ N2 = 40, Mixed Classes ]
            [ Gini(D1) = 0.00       ]   [ Gini(D2) = 0.38        ]
            (Terminal Leaf Node)                 │
                                    Feature Split: x2 ≤ 12.0 ?
                                     ┌───────────┴───────────┐
                                  Yes│                       │No
                                     ▼                       ▼
                                [ Leaf Node ]           [ Leaf Node ]
```

##### Structural Comparison: Decision Tree Induction Algorithms

| Algorithm Feature | ID3 Algorithm | C4.5 Algorithm | CART Algorithm |
| :--- | :--- | :--- | :--- |
| **Splitting Criterion** | Information Gain | Gain Ratio | Gini Index (Class) / MSE (Reg) |
| **Tree Structure** | Multi-way splitting ($>2$ branches) | Multi-way splitting | **Strict Binary Splitting** (2 branches) |
| **Supported Attributes** | Categorical features only | Categorical & Continuous features | Categorical & Continuous features |
| **Missing Value Handling** | No native support | Native probabilistic imputation | Native surrogate split rules |
| **Pruning Strategy** | None (grows full tree) | Post-pruning (Error-based) | Cost-Complexity Pruning ($R_\alpha(T)$) |

---

#### 3. Part (b): Overfitting Mitigation via Tree Pruning

Unconstrained decision trees tend to memorize noisy training samples, creating deep complex structures with low bias but extremely high variance.

##### 1. Pre-Pruning (Early Stopping)
Halts tree growth prematurely during construction if specific hyperparameter thresholds are triggered:
* `max_depth`: Limits the maximum vertical distance between root and leaf nodes.
* `min_samples_split`: Enforces a minimum number of samples required to split an internal node.
* `min_samples_leaf`: Mandates a minimum sample count in terminal leaf nodes.
* `min_impurity_decrease`: Disallows splits that produce impurity gains lower than threshold $\epsilon$.

##### 2. Post-Pruning (Cost-Complexity Pruning)
Grows a fully unconstrained tree $T_0$ first, then systematically collapses non-significant subtrees using Minimal Cost-Complexity Pruning. The cost-complexity measure $R_\alpha(T)$ balances empirical error against tree size:

$$R_\alpha(T) = R(T) + \alpha |T|$$

Where $R(T)$ represents total subtree classification error, $|T|$ is the count of terminal leaf nodes, and $\alpha \ge 0$ is the complexity tuning parameter. Increasing $\alpha$ penalizes complex trees, pruning weak subtrees to improve generalization performance.

---

### Question 4 (10 Marks):
**(a) Contrast Bagging and Boosting ensemble paradigms. Explain Random Forest and feature subspace sampling.**  
**(b) Detail the AdaBoost algorithm step-by-step, including sample re-weighting formulas and classifier aggregation.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **Ensemble Theory & Bagging vs Boosting** | Variance reduction vs. Bias reduction mechanisms, parallel vs. sequential training pipelines. | **3 Marks** |
| **Random Forest Framework** | Bootstrap sampling, Out-Of-Bag (OOB) error estimation, and random feature subspace selection. | **2 Marks** |
| **AdaBoost Mathematical Steps** | Weight initialization, error rate $\epsilon_t$, estimator weight $\alpha_t$, sample re-weighting, and normalization. | **3 Marks** |
| **XGBoost & Gradient Boosting Overview** | Residual fitting, second-order Taylor expansion gradients, and comparative matrix. | **2 Marks** |

---

#### 2. Part (a): Bagging vs. Boosting & Random Forest

##### Ensemble Learning Theory
Ensemble learning combines predictions from multiple base models (weak learners) to build a unified estimator achieving superior predictive accuracy and robustness.

##### Bagging (Bootstrap Aggregating)
Bagging reduces model **Variance** without increasing bias. Base estimators are trained independently in **parallel** on randomized bootstrap subsets sampled with replacement from the training dataset. Predictions are combined using majority voting (classification) or uniform averaging (regression).

##### Boosting
Boosting reduces model **Bias** (and variance). Base estimators are trained **sequentially**; each new weak estimator focuses on correcting the residual errors and misclassifications committed by prior models through adaptive instance re-weighting.

##### Random Forest Classifier
Random Forest enhances Bagging by introducing **Feature Subspace Sampling** (Random Patches) to decorrelate individual decision trees:
1. **Bootstrap Instance Sampling:** Each tree is trained on an independent dataset $D_b$ constructed by uniform sampling with replacement ($N$ samples).
2. **Feature Subspace Selection:** At each node split, instead of evaluating all $n$ features, the algorithm considers a randomized subset of $m = \sqrt{n}$ features.
3. **Out-Of-Bag (OOB) Error:** Approximately $1 - \frac{1}{e} \approx 36.8\%$ of training samples are left out of each bootstrap set $D_b$. These OOB samples serve as a built-in cross-validation test set to evaluate model performance without requiring an external validation split.

##### ASCII Architectural Comparison Diagram: Bagging vs. Boosting
```
BAGGING (Parallel Architecture):
  [ Training Data D ]
     ├──► Bootstrap Sample D1 ──► [ Model 1 ] ──┐
     ├──► Bootstrap Sample D2 ──► [ Model 2 ] ──┼──► [ Majority Vote / Average ] ──► Final Output
     └──► Bootstrap Sample D3 ──► [ Model 3 ] ──┘

BOOSTING (Sequential Architecture):
  [ Data D ] ──► [ Model 1 ] ──► [ Error Calculation & Weight Adjustment ]
                                               │
                                               ▼
                 [ Weighted Data D2 ] ──► [ Model 2 ] ──► [ Weight Adjustment ]
                                                                      │
                                                                      ▼
                                       [ Weighted Data D3 ] ──► [ Model 3 ]
                                                                      │
                                                                      ▼
                                                       [ Weighted Combination ∑ α_t * h_t(x) ]
```

---

#### 3. Part (b): Mathematical Derivation of AdaBoost Algorithm

AdaBoost (Adaptive Boosting) trains sequence $T$ of weak decision stumps $h_t(\mathbf{x}) \in \{-1, +1\}$ on weighted training samples.

##### Step-by-Step Algorithmic Process

**Step 1: Initialize Sample Weights**
For dataset containing $M$ samples $\{( \mathbf{x}^{(i)}, y^{(i)} )\}_{i=1}^M$ where $y^{(i)} \in \{-1, +1\}$, initialize equal sample weights:

$$w_{1, i} = \frac{1}{M} \quad \text{for } i = 1, 2, \dots, M$$

**Step 2: Sequential Iterative Training (For $t = 1, 2, \dots, T$)**

1. Fit weak estimator $h_t(\mathbf{x})$ using current sample weight distribution $\mathbf{w}_t$.
2. Calculate Weighted Error Rate $\epsilon_t$:
   $$\epsilon_t = \frac{\sum_{i=1}^{M} w_{t, i} \cdot \mathbb{I}\left( y^{(i)} \ne h_t(\mathbf{x}^{(i)}) \right)}{\sum_{i=1}^{M} w_{t, i}}$$
   Where $\mathbb{I}(\cdot)$ is the indicator function.

3. Compute Estimator Importance Weight $\alpha_t$:
   $$\alpha_t = \frac{1}{2} \ln\left( \frac{1 - \epsilon_t}{\epsilon_t} \right)$$
   If $\epsilon_t \le 0.5$, $\alpha_t > 0$. Accurate estimators gain higher voting influence.

4. Update Sample Weights for Next Iteration ($w_{t+1, i}$):
   $$w_{t+1, i} = w_{t, i} \cdot \exp\left( -\alpha_t \cdot y^{(i)} \cdot h_t(\mathbf{x}^{(i)}) \right)$$
   *   If misclassified ($y^{(i)} h_t(\mathbf{x}^{(i)}) = -1 \implies \exp(+\alpha_t)$): Weight increases.
   *   If correctly classified ($y^{(i)} h_t(\mathbf{x}^{(i)}) = +1 \implies \exp(-\alpha_t)$): Weight decreases.

5. Normalize Sample Weights:
   $$Z_t = \sum_{i=1}^{M} w_{t+1, i}, \quad w_{t+1, i} := \frac{w_{t+1, i}}{Z_t}$$

**Step 3: Final Aggregated Prediction**
The overall ensemble decision is a weighted majority sign combination:

$$H(\mathbf{x}) = \text{sign}\left( \sum_{t=1}^{T} \alpha_t h_t(\mathbf{x}) \right)$$

##### Comparison Matrix: Ensemble Paradigms

| Attribute | Bagging (Random Forest) | AdaBoost | Gradient Boosting / XGBoost |
| :--- | :--- | :--- | :--- |
| **Build Architecture** | **Parallel** independent training | **Sequential** iterative updates | **Sequential** residual optimization |
| **Primary Targeted Error**| Reduces **Variance** | Reduces **Bias** | Reduces **Bias and Variance** |
| **Base Estimator Type** | Fully grown deep decision trees | Shallow decision stumps | Shallow regression trees |
| **Sampling Mechanism** | Bootstrap random sampling | Adaptive sample re-weighting | Gradient-based sample selection |
| **Aggregation Rule** | Unweighted majority voting | Weighted sum ($\sum \alpha_t h_t$) | Gradient descent line search sum |
| **Outlier Sensitivity** | Low (highly robust to noise) | High (amplifies outlier weights) | Moderately high (controlled by learning rate) |

---

### Question 5 (10 Marks):
**(a) Explain the K-Nearest Neighbors (KNN) non-parametric classification algorithm. Discuss distance metrics and the effect of hyperparameter $K$.**  
**(b) Derive the Support Vector Machine (SVM) Maximum Margin formulation. Explain Soft Margin SVM, slack variables $\xi_i$, and the Kernel Trick.**

---

#### 1. Mumbai University Marking Scheme Rubric (10 Marks)

| Sub-Component | Evaluation Criteria | Allocated Marks |
| :--- | :--- | :--- |
| **KNN Principles** | Lazy learning concept, distance metrics (Euclidean, Manhattan, Minkowski), and choice of $K$. | **2.5 Marks** |
| **SVM Maximum Margin Derivation** | Decision boundary geometry, margin distance $2/\|\mathbf{w}\|$, and primal optimization formulation. | **3 Marks** |
| **Soft-Margin & Slack Variables** | Hinge Loss, trade-off parameter $C$, slack variables $\xi_i$, and non-separable handling. | **2.5 Marks** |
| **Kernel Trick & Mercer's Theorem** | Feature space mapping $\phi(\mathbf{x})$, Kernel functions (RBF, Polynomial, Linear), and comparison. | **2 Marks** |

---

#### 2. Part (a): K-Nearest Neighbors (KNN) Classification

##### Lazy Learning Principle
KNN is a non-parametric instance-based (lazy learning) algorithm that defers model training until query time, storing training observations directly in memory.

##### Distance Metric Formulations
Given query instance $\mathbf{x}^*$ and training sample $\mathbf{x}^{(i)} \in \mathbb{R}^n$:

1. **Euclidean Distance ($L_2$ Norm):**
   $$d(\mathbf{x}^*, \mathbf{x}^{(i)}) = \sqrt{\sum_{j=1}^{n} (x_j^* - x_j^{(i)})^2}$$

2. **Manhattan Distance ($L_1$ Norm):**
   $$d(\mathbf{x}^*, \mathbf{x}^{(i)}) = \sum_{j=1}^{n} |x_j^* - x_j^{(i)}|$$

3. **Minkowski Distance ($L_p$ Norm Generalized):**
   $$d(\mathbf{x}^*, \mathbf{x}^{(i)}) = \left( \sum_{j=1}^{n} |x_j^* - x_j^{(i)}|^p \right)^{1/p}$$

##### Impact of Hyperparameter $K$ Selection
*   **Small $K$ (e.g., $K=1$):** Low bias, extremely high variance; highly sensitive to noise and outliers (overfitting).
*   **Large $K$ (e.g., $K=N$):** High bias, low variance; over-simplifies boundaries, predicting the majority global class (underfitting).
*   *Optimal $K$:* Typically selected via $K$-fold cross-validation (often choosing odd values for binary classification to break ties).

---

#### 3. Part (b): Support Vector Machines (SVM) & Kernel Methodologies

##### Hard-Margin SVM Formulation
SVM identifies an optimal separating hyperplane $\mathbf{w}^T \mathbf{x} + b = 0$ that maximizes the geometric margin $\gamma = \frac{2}{\|\mathbf{w}\|}$ separating binary classes ($y_i \in \{-1, +1\}$).

##### ASCII Diagram: SVM Maximum Margin & Support Vectors
```
                           Hyperplane: w^T x + b = +1 (Positive Margin Boundary)
                                     ╱
        (Positive Class +1)        ╱   • Support Vector (x_i)
                 +               ╱
                       +       ╱
─────────────────────────────┼──────────────────────────────
                           ╱   Margin Width = 2 / ||w||
                         ╱
          -            ╱
                 -   ╱         • Support Vector (x_i)
        (Negative Class -1)  ╱
                           Hyperplane: w^T x + b = -1 (Negative Margin Boundary)
```

##### Primal Quadratic Optimization Problem
Maximizing margin $\frac{2}{\|\mathbf{w}\|}$ is mathematically equivalent to minimizing $\frac{1}{2} \|\mathbf{w}\|^2$ subject to strict linear margin constraints:

$$\min_{\mathbf{w}, b} \frac{1}{2} \|\mathbf{w}\|^2 \quad \text{subject to} \quad y^{(i)} (\mathbf{w}^T \mathbf{x}^{(i)} + b) \ge 1, \quad \forall i = 1, \dots, m$$

##### Soft-Margin SVM & Slack Variables ($\xi_i$)
To handle linearly non-separable or noisy datasets, Soft-Margin SVM introduces slack variables $\xi_i \ge 0$ allowing limited constraint violations, controlled by penalty hyperparameter $C$:

$$\min_{\mathbf{w}, b, \boldsymbol{\xi}} \frac{1}{2} \|\mathbf{w}\|^2 + C \sum_{i=1}^{m} \xi_i \quad \text{subject to} \quad y^{(i)} (\mathbf{w}^T \mathbf{x}^{(i)} + b) \ge 1 - \xi_i, \quad \xi_i \ge 0$$

*   **Large $C$:** High penalty for misclassifications $\implies$ Narrower margin (risk of overfitting).
*   **Small $C$:** Tolerates misclassifications $\implies$ Wider margin (risk of underfitting).

##### The Kernel Trick
When data cannot be separated linearly in original input space $\mathbb{R}^n$, it is transformed into a higher-dimensional feature space $\mathcal{H}$ via mapping function $\phi(\mathbf{x})$.

By applying **Mercer's Theorem**, the dual optimization problem depends solely on inner products $\phi(\mathbf{x}_i)^T \phi(\mathbf{x}_j)$. A Kernel Function $K(\mathbf{x}_i, \mathbf{x}_j)$ calculates this inner product directly in lower-dimensional space without explicitly computing non-linear transformation $\phi(\cdot)$:

$$K(\mathbf{x}_i, \mathbf{x}_j) = \phi(\mathbf{x}_i)^T \phi(\mathbf{x}_j)$$

##### Common Kernel Functions
1. **Linear Kernel:** $K(\mathbf{x}_i, \mathbf{x}_j) = \mathbf{x}_i^T \mathbf{x}_j$
2. **Polynomial Kernel:** $K(\mathbf{x}_i, \mathbf{x}_j) = (\mathbf{x}_i^T \mathbf{x}_j + c)^d$
3. **Radial Basis Function (RBF / Gaussian) Kernel:**
   $$K(\mathbf{x}_i, \mathbf{x}_j) = \exp\left( -\gamma \|\mathbf{x}_i - \mathbf{x}_j\|^2 \right) \quad (\text{where } \gamma = \frac{1}{2\sigma^2})$$

---

## Examination Preparation Summary Matrix: Module 02

| Question Focus | Core Algorithmic Concepts | Primary Mathematical Formulas | Essential Evaluation Focus |
| :--- | :--- | :--- | :--- |
| **Linear Regression & Regularization** | OLS Minimization, Normal Equation, Gradient Descent, $L_1/L_2$ Penalties | $\mathbf{w}^* = (\mathbf{X}^T \mathbf{X})^{-1} \mathbf{X}^T \mathbf{y}$, $J(\mathbf{w}) + \lambda \|\mathbf{w}\|$ | MSE, Normal Eq Derivation, Sparsity |
| **Logistic Regression & Naive Bayes** | Sigmoid mapping, MLE Log Loss, Bayes' Theorem, Conditional Independence | $p = \frac{1}{1+e^{-z}}$, $-\frac{1}{m} \sum [y \ln \hat{y} + (1-y)\ln(1-\hat{y})]$ | Logit derivation, MLE steps, NB variants |
| **Decision Trees (CART/ID3)** | Impurity metrics, Recursive binary splitting, Tree pruning | $\text{Gini} = 1 - \sum p_k^2$, $\text{Entropy} = -\sum p_k \log_2 p_k$ | Gini vs Gain, Cost-Complexity Pruning |
| **Ensemble Learning Paradigms** | Bagging vs Boosting, Random Forest, AdaBoost, XGBoost | $\alpha_t = \frac{1}{2}\ln\left(\frac{1-\epsilon_t}{\epsilon_t}\right)$, $w_{t+1} = w_t e^{-\alpha y h(x)}$ | Variance vs Bias, AdaBoost derivation |
| **KNN & Support Vector Machines** | Distance metrics, Maximum Margin, Soft Margin, Kernel Trick | $\min \frac{1}{2}\|\mathbf{w}\|^2 + C\sum \xi_i$, $K(\mathbf{x}_i, \mathbf{x}_j) = e^{-\gamma \|\mathbf{x}_i - \mathbf{x}_j\|^2}$ | Margin geometry, Slack $C$, RBF Kernel |

---
