# Options Pricer

Academic project from ENSAE Paris implementing a comprehensive options pricing framework with support for European, American, and Asian options using analytical and numerical methods.

## What It Demonstrates

- **Black-Scholes pricing** for European options with dividend adjustments (lump sum and continuous dividends)
- **Longstaff-Schwartz Monte Carlo** (LSM) algorithm for American option pricing with early exercise
- **Monte Carlo simulation** for Asian (arithmetic average) options
- **Object-oriented design** in C++ with inheritance and polymorphism for extensible option types
- **Asset modeling** with support for dividends, volatility, and risk-free rate dynamics
- **Interactive pricing tool** with command-line interface for real-time option valuation

## Key Results

- Full implementation of three major option types (European, American, Asian) with both call and put support
- Efficient numerical methods: analytical solutions where available, Monte Carlo with 10,000+ paths for path-dependent options
- Dividend handling: supports no dividends, lump sum dividends, and continuous dividend yield
- Detailed report available in [`reports/rapport_pricer.pdf`](reports/rapport_pricer.pdf) with methodology, results, and analysis

## Repository Layout

```
options_pricer_project/
├── src/                    # Source code
│   ├── main.cpp           # Interactive pricing application
│   ├── option.hpp/cpp     # Base option class
│   ├── european.hpp/cpp   # European option implementation
│   ├── american.hpp/cpp   # American option (LSM algorithm)
│   ├── asian.hpp/cpp      # Asian option (Monte Carlo)
│   ├── asset.hpp/cpp      # Underlying asset model
│   └── tools.hpp/cpp      # Numerical utilities (cdf, regression, simulation)
├── reports/                # Documentation and analysis
│   └── rapport_pricer.pdf # Project report
├── notebooks/              # Analysis notebooks (optional)
├── data/                   # Data directory (see data/README.md)
├── tests/                  # Unit tests (optional)
├── LICENSE                 # MIT License
├── requirements.txt        # Dependencies
└── README.md              # This file
```

## Quickstart

### Prerequisites

- C++ compiler with C++11 support (g++ or clang++)
- Eigen3 library for matrix operations

**Install Eigen3:**
```bash
# macOS
brew install eigen

# Ubuntu/Debian
sudo apt-get install libeigen3-dev

# Or download from https://eigen.tuxfamily.org/
```

### Build and Run

```bash
# Compile the project
g++ -std=c++11 -I/usr/local/include/eigen3 -I./src src/*.cpp -o pricer

# Run the interactive pricer
./pricer
```

### Demo Example

The program provides an interactive interface. Example workflow:

1. Enter risk-free rate (e.g., `5` for 5%)
2. Select option type: `eu` (European), `am` (American), or `as` (Asian)
3. Input option parameters when prompted:
   - Current time, spot price, volatility
   - Strike price, maturity
   - Position (call/put)
   - Dividend information (if applicable)
4. Choose action:
   - `p` - Price the option
   - `e` - Estimate future asset price
   - `n` - Create new option
   - `q` - Quit

**Example pricing a European call:**
```
Risk free rate: 5
Option type: eu
Current time: 0
Spot price: 100
Volatility: 0.2
Dividend type (0=none, 1=lump, 2=continuous): 0
Strike: 100
Maturity: 1
Position (call/put): call
Action: p
```

## Method Overview

### European Options
- **Method**: Analytical Black-Scholes formula
- **Dividend handling**: 
  - Lump dividends: Adjusted spot price using `S_hat = S * (1 - d)^n`
  - Continuous dividends: Adjusted strike using `K_hat = K * exp(q*T)`
- **Put pricing**: Uses call-put parity

### American Options
- **Method**: Longstaff-Schwartz Monte Carlo (LSM) algorithm
- **Simulation**: 10,000 paths with 1,000 time steps
- **Regression**: Second-order polynomial regression for continuation value estimation
- **Early exercise**: Optimal stopping decision at each time step
- **Limitation**: Currently supports only non-dividend paying assets

### Asian Options
- **Method**: Monte Carlo simulation (10,000 paths, 1,000 time steps per path)
- **Payoff**: Arithmetic average of underlying price over option lifetime
- **Limitation**: Currently supports only non-dividend paying assets

## Notes and Limitations

- **American options**: Dividend-paying assets not yet supported
- **Asian options**: Dividend-paying assets not yet supported
- **Performance**: American option pricing may take several minutes due to Monte Carlo simulation
- **Numerical precision**: Monte Carlo methods subject to sampling error; increase simulation paths for higher accuracy
- **Input validation**: Basic validation present; ensure realistic parameter ranges

## References

- Black, F., & Scholes, M. (1973). The pricing of options and corporate liabilities. *Journal of Political Economy*, 81(3), 637-654.
- Longstaff, F. A., & Schwartz, E. S. (2001). Valuing American options by simulation: a simple least-squares approach. *The Review of Financial Studies*, 14(1), 113-147.
- Hull, J. C. (2018). *Options, Futures, and Other Derivatives* (10th ed.). Pearson.

## Contact

For questions or contributions, please open an issue or contact the repository maintainer.