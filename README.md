# Time-Series Forecasting of NYSE Stocks with LSTM

---

## Executive Summary
This project predicts future stock prices using Long Short-Term Memory (LSTM) neural networks on New York Stock Exchange (NYSE) data. Multiple batch sizes were tested to evaluate the model’s performance, with results indicating that smaller batch sizes, particularly 32, provided the most accurate predictions with minimal overfitting. The findings suggest that deep learning can effectively capture patterns in volatile financial data when carefully tuned.

---

## Business Problem
How can we accurately forecast stock prices in a market that is highly volatile and influenced by complex temporal patterns?  

Investors, traders, and financial analysts need reliable predictions to make informed decisions, manage risk, and optimize trading strategies. Traditional methods often struggle to capture the rapidly changing nature of stock prices, leading to overfitting on historical data or underfitting when the model fails to learn patterns. This project explores whether LSTM neural networks can effectively model these temporal dependencies to provide actionable predictions.

**Objective:** Predict the next-day closing price of NYSE-listed stocks.  
**Challenges:** High market volatility, temporal dependencies, and overfitting on historical data.  

---

## Methodology

### Data
- **Source:** New York Stock Exchange (CSV dataset)  
- **Columns:** Date, Open, High, Low, Close, Volume  
- **Preprocessing:**  
  - Checked and handled missing values  
  - Normalized data to scale stock prices for model training  

### Model
- **Architecture:** LSTM (Long Short-Term Memory) neural network  
- **Hyperparameters Tested:**  
  - Batch sizes: 512, 128, 64, 32  
  - Optimizer: Adam  
  - Loss function: Mean Squared Error (MSE)  
- **Training/Test Split:** 80/20 ratio
- **Evaluation Metrics:** MSE, RMSE  

### Experiment & Results

| Batch Size | Train MSE | Train RMSE | Test MSE | Test RMSE |
|------------|-----------|------------|----------|-----------|
| 512        | 0.01862   | 0.14       | 0.00409  | 0.06      |
| 128        | 0.00740   | 0.09       | 0.01965  | 0.14      |
| 64         | 0.00568   | 0.08       | 0.01349  | 0.12      |
| 32         | 0.00047   | 0.02       | 0.00110  | 0.03      |


<img width="909" height="475" alt="image" src="https://github.com/user-attachments/assets/2ec70634-7c5b-47a4-8628-2cb4d3286535" />

### Key Findings
- **Batch Size 32:**  
  - Achieved the lowest training and testing error, indicating excellent generalization.  
  - Minimal gap between training and testing metrics suggests low overfitting and high reliability for unseen data.  
  - Demonstrates the ability of small batch sizes to adapt to high volatility and rapidly changing market conditions.  

- **Batch Size 64:**  
  - Moderate performance with slightly higher errors than batch 32.  
  - Training and testing metrics indicate reasonable generalization, making it a good alternative when computational resources are limited.  
  - Suitable for practical implementations where smaller batches may be computationally expensive.  

- **Batch Size 512:**  
  - Surprisingly low test MSE but high training MSE indicates underfitting.  
  - The model struggles to learn the training data adequately due to too-large batch updates, but still captures some general patterns.  
  - Highlights that larger batch sizes may fail to capture fine-grained temporal dependencies in volatile stock data.  

- **Batch Size 128:**  
  - Worst test performance with a large gap between training and testing errors, indicative of overfitting.  
  - Model memorizes training patterns rather than generalizing to unseen data.  
  - Suggests the need for stronger regularization or adjustments to learning rate and architecture when using medium batch sizes.  

**Overall Insight:**  
Smaller batch sizes (32–64) outperform larger ones in volatile financial datasets due to better adaptability to rapid market changes. Batch size 32 provides the best balance of accuracy, generalization, and stability, making it the optimal choice for this LSTM stock predictor.

### Potential Improvements
- Add more LSTM layers to capture complex temporal dependencies  
- Experiment with different learning rates and optimizers  
- Incorporate additional features such as technical indicators or market sentiment  
- Use regularization techniques like dropout to further reduce overfitting  


