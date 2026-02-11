# Assignment 2 – Probability Density Estimation with Generative Adversarial Networks

## 📌 Project Summary
This assignment focuses on estimating the probability density function (PDF) of an unknown random variable using only observed data samples. Rather than assuming any predefined analytical distribution, a Generative Adversarial Network (GAN) is trained to learn the data distribution directly from samples.

The experiment is conducted using real-world NO₂ concentration data. A nonlinear transformation is applied to the data before training the GAN, allowing the model to capture complex distributional patterns.

---

## 📊 Dataset Description
- **Feature Used:** NO₂ concentration  
- **Data Source:** India Air Quality Dataset (Kaggle)  
- **Preprocessing Steps:**
  - Extracted only the NO₂ column
  - Removed missing and invalid values
  - Normalized the data prior to training

---

## 🔄 Nonlinear Data Transformation
Each original NO₂ value \( x \) is transformed into a new variable \( z \) using the following function:

\[
z = x + a_r \sin(b_r x)
\]

where:
- \( r \) denotes the university roll number  
- \( a_r = 0.5 \times (r \bmod 7) \)  
- \( b_r = 0.3 \times ((r \bmod 5) + 1) \)

### Parameters Used (Roll Number: 102497010)
- \( a_r = 1.5 \)  
- \( b_r = 0.6 \)

Final transformation applied:
\[
z = x + 1.5 \sin(0.6x)
\]

---

## 📈 Distribution of Transformed Data
The empirical distribution of the transformed variable \( z \) is visualized below.

![Transformed Distribution](screenshots/Screenshot%202026-02-11%20215522.png)

---

## 🧠 GAN Architecture

### Generator
- **Input:** Random noise sampled from a standard normal distribution
- **Output:** Synthetic samples of the transformed variable
- **Architecture:** Fully connected neural network with ReLU activations

### Discriminator
- **Input:** Real or generated samples
- **Output:** Probability that the input sample is real
- **Architecture:** Fully connected neural network with a Sigmoid activation at the output layer

---

## ⚙️ Training Configuration
- **Loss Function:** Binary Cross-Entropy  
- **Optimizer:** Adam  
- **Learning Rate:** 0.001  
- **Epochs:** 3000  
- **Batch Size:** 128  

No parametric probability distribution (such as Gaussian or exponential) is assumed during the training process.

---

## 🧪 Probability Density Estimation
After completing GAN training:
1. A large number of samples are generated using the trained generator
2. Kernel Density Estimation (KDE) is applied to these samples to approximate the PDF

---

## 📉 PDF Approximation Results
The following plot compares:
- The empirical distribution of the transformed data
- The estimated PDF obtained from GAN-generated samples

![Screenshot](screenshots/Screenshot%202026-02-11%20215504.png)

---

## 🔍 Key Observations
- The GAN successfully learns the overall shape of the transformed data distribution
- Training becomes stable after the initial epochs
- No major mode collapse is observed
- Small discrepancies appear in the tail regions due to limited sample size
- The distribution is learned purely from data without assuming an analytical PDF

---

## ✅ Conclusion
This assignment demonstrates that Generative Adversarial Networks can effectively approximate unknown probability density functions using only observed samples. The generator learns to map random noise to realistic data points, while the discriminator guides learning through adversarial feedback.

---

## 🛠 Tools and Libraries
- Python  
- NumPy  
- Pandas  
- Matplotlib  
- Scikit-learn  
- PyTorch  
