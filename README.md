# SX5E Local Volatility Calibration: Andreasen-Huge Algorithm

This project focuses on calibrating a **Local Volatility model** to the EURO STOXX 50 (SX5E) index. Using the **Andreasen-Huge (2010)** algorithm, the project builds an arbitrage-free implied volatility surface by interpolating market data and extrapolating smiles for future maturities ($T=1$ and $T=1.5$).

## 📌 Project Overview

The objective of this project is to implement a robust numerical scheme that matches a discrete set of market-quoted European call option prices and produces a continuous, consistent volatility surface. Unlike traditional Dupire local volatility models that require a smooth input surface, the Andreasen-Huge approach uses a fully implicit finite-difference scheme to calibrate a piecewise-constant volatility function directly.

### Key Features:

* **Arbitrage-Free Calibration**: Ensures the resulting price surface is monotone in maturity and decreasing in strike.
* **Numerical Optimization**: Utilizes Least Squares and the L-BFGS-B optimizer to calibrate the volatility parameters ($\theta$).
* **Surface Interpolation & Extrapolation**: Successfully back-out implied volatilities for $T=1.0$ and $T=1.5$ maturities.
* **Visualization**: Interactive 3D surface plots for both call prices and implied volatilities.

## 📂 Repository Structure

```text
├── data/
│   └── SX5E_Impliedvols.xlsx       # Market implied volatility matrix for SX5E
├── papers/
│   ├── Andreasen-Huge_2010.pdf     # "Volatility Interpolation" (Original Paper)
│   └── Fernandez_SABR_2024.pdf     # Reference on SABR calibration methods
├── analysis.ipynb                  # Full implementation (Python/Jupyter)
├── project_report.pdf              # Detailed mathematical derivation and analysis
├── requirements.txt                # Python dependencies
└── README.md                       # Project documentation

```

## 🛠 Methodology

The implementation follows these core steps:

1. **Data Setup**: Market IVs are mapped to an absolute strike grid ($S_0 = 100$) with $r=q=0$.


2. **Price Conversion**: Implied volatilities are converted to Black-Scholes call prices to serve as targets for the calibration.


3. **The AH Step**: Between consecutive expiries, a one-step fully implicit finite difference scheme is used to propagate the price vector.


4. **Calibration**: A piecewise-constant volatility function $\theta(K)$ is optimized at each maturity layer to minimize the squared error between model and market prices.


5. **Volatility Inversion**: Final prices are inverted back into implied volatilities using the Nelder-Mead algorithm to visualize the resulting "smiles".


## 📈 Results

The model successfully reproduces the characteristic "smile" and "skew" observed in the SX5E market data. The extrapolated smiles for $T=1$ and $T=1.5$ integrate smoothly into the existing term structure without introducing spurious oscillations or calendar arbitrage.

---

**Authors:** [BOURGON Elias, DECAUX Théodore, SANTANGELO Jason] 

**Date:** October 2025
