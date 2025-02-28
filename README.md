# Bonds

# Bond Market Analysis Toolkit

A comprehensive Python toolkit for analyzing, pricing, and predicting risks in the bond market.

## Features

- **Bond Yield Calculation**: Compute the Yield to Maturity (YTM) of bonds using the Newton-Raphson method
- **Bond Price Calculation**: Calculate bond prices based on coupon rates, maturity, and yield
- **Yield Curve Analysis**: Analyze and visualize yield spreads and curves
- **Corporate Default Prediction**: Assess default risk using multiple approaches:
  - Altman Z-Score calculation
  - Machine learning-based probability of default

## Installation

```bash
# Clone the repository
git clone https://github.com/yourusername/bond-market-analysis.git
cd bond-market-analysis

# Install required packages
pip install -r requirements.txt
```

## Required Dependencies

- numpy
- pandas
- matplotlib
- seaborn
- scikit-learn
- scipy

## Usage Examples

### Bond Yield to Maturity Calculation

```python
from bond_analysis import bond_ytm

# Input values
bond_price = 100  # Market price 
face_value = 100  # Face value 
coupon_rate = 0.06  # 6% annual coupon rate 
years_to_maturity = 10  # 10 years to maturity 

# Calculate the YTM
ytm = bond_ytm(bond_price, face_value, coupon_rate, years_to_maturity)
print(f"Yield to Maturity: {ytm:.2%}")
```

### Bond Price Calculation

```python
from bond_analysis import bond_price

# Input values 
face_value = 100
coupon_rate = 0.06  # 6% annual coupon rate
years_to_maturity = 10 
ytm = 0.06  # 6% yield to maturity

# Calculate the bond price
price = bond_price(face_value, coupon_rate, years_to_maturity, ytm)
print(f"Bond Price: ${price:.2f}")
```

### Yield Curve Analysis

```python
import pandas as pd
import matplotlib.pyplot as plt
from bond_analysis import analyze_yield_curve

# Load your treasury rates data
data = pd.read_csv("daily-treasury-rates.csv")

# Analyze yield spreads
analyze_yield_curve(data)
```

### Corporate Default Risk Assessment

#### Altman Z-Score

```python
from bond_analysis import altman_z_score

# Company financial metrics
Z, risk_level = altman_z_score(
    working_capital=215000000, 
    total_assets=940000000,
    retained_earnings=-105000000, 
    ebit=-127000000,
    market_value_equity=410000000,
    total_liabilities=973000000, 
    sales=760000000
)

print(f"Altman Z-score: {Z:.2f}, Risk Level: {risk_level}")
```

#### Machine Learning Default Prediction

```python
import numpy as np
from bond_analysis import predict_default_probability

# Example bond features
new_bond = np.array([[
    4.0,   # Debt to Equity
    1.5,   # Interest Coverage
    5.0,   # Profit Margin
    1.2,   # Current Ratio
    1.5,   # Altman Z-Score
    50.0,  # Stock Volatility
    300.0, # CDS Spread
    5.0,   # Bond Maturity
    2.0    # Industry Sector
]])

# Predict probability of default
default_probability = predict_default_probability(new_bond)
print(f"Predicted Default Probability: {default_probability:.2%}")
```

## Methodology

### Yield to Maturity

The YTM is calculated using the Newton-Raphson method to find the discount rate that makes the present value of all future cash flows equal to the current market price.

### Altman Z-Score

The Altman Z-Score uses five financial ratios to predict the probability of bankruptcy:

- **X1**: Working Capital / Total Assets (Liquidity)
- **X2**: Retained Earnings / Total Assets (Profitability over time)
- **X3**: EBIT / Total Assets (Operating efficiency)
- **X4**: Market Value of Equity / Total Liabilities (Solvency)
- **X5**: Sales / Total Assets (Asset turnover)

**Interpretation**:
- Z > 2.99: "Safe" Zone
- 1.81 < Z < 2.99: "Gray" Zone
- Z < 1.81: "Distress" Zone

### Default Prediction Model

The default prediction model uses logistic regression trained on various financial metrics:
- Debt-to-Equity ratio
- Interest coverage ratio
- Profit margin
- Current ratio
- Altman Z-Score
- Stock volatility
- Credit Default Swap (CDS) spread
- Bond maturity
- Industry sector

## Data Requirements

The yield curve analysis requires a CSV file with treasury rates including columns for dates and yields of different maturities (3 Mo, 1 Yr, 5 Yr, 10 Yr, 30 Yr).

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is licensed under the MIT License - see the LICENSE file for details.
