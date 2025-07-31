# Multi-Asset Spot and Option Market Simulation & Deep Hedging (Reproduction of Wiese et al., 2021)

This project is a **reproduction and extension** of [Wiese et al. (2021): "Multi-Asset Spot and Option Market Simulation"](https://arxiv.org/abs/2112.06823).

It includes:

- Construction of **arbitrage-free synthetic call price surfaces** from real spot data (Amazon, Apple).
- Market simulation using **normalizing flows** and autoencoders, as in the paper.
- Creation of both **single-asset and multi-asset spot price simulators**.
- **Deep Hedging** via reinforcement learning, applied to the payoff of a basket option on these assets with transaction cost.
- All code is in Jupyter Notebooks; data includes `.ipynb` notebooks and Excel files.

---

## Methodology

### 1. Synthetic Call Price Grids

- **Purpose:** Overcome the lack of historical option price data by constructing **arbitrage-free synthetic call price surfaces**.
- **Process:**  
  - Use spot prices (Amazon, Apple) to generate call option grids for a range of strikes and maturities.
  - Ensure no static arbitrage via DLV (Discrete Local Volatility) methods as described in [Wiese et al., 2021].
  - Use Excel files for storage and manipulation.

### 2. Spot Price Simulator

- **Purpose:** Model realistic single-asset spot price dynamics.
- **Process:**  
  - Use actual spot price data from Amazon (and Apple).
  - Build a normalizing flow-based simulator that learns the conditional dynamics of spot returns and call surface features.
  - Apply autoencoder for efficient, low-dimensional encoding of synthetic call grids.

### 3. Multi-Asset Simulator

- **Purpose:** Simulate joint evolution of multiple assets (Amazon + Apple).
- **Process:**  
  - Train individual simulators on each asset.
  - Model the joint latent space with a Gaussian copula, following the multi-asset method in the paper.
  - Allows for the simulation of **basket options** and multi-asset hedging scenarios.

### 4. Deep Hedging RL (**Custom Implementation**)

- **Purpose:** Apply reinforcement learning to **hedge the payoff** of a basket option on the simulated multi-asset market with transaction cost.
- **Process:**  
  - **Implemented a custom deep RL neural network** for hedging, inspired by the deep hedging framework but built from scratch for this project.
  - Uses generated price paths from the simulators as the environment for training with transaction costs.
  - The RL agent learns trading strategies to minimize risk and optimize hedging performance.


