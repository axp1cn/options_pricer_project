# Data Directory

This directory is reserved for datasets and market data used in options pricing.

## Usage

Place any data files here that are needed for:
- Historical price data
- Volatility surfaces
- Market calibration data
- Test cases and benchmarks

## Important Notes

- **Do not commit large datasets** to the repository
- Use `.gitignore` to exclude data files from version control
- For public datasets, provide download instructions in this README
- For proprietary data, document the data format and structure only

## Example Data Structure

```
data/
├── README.md (this file)
├── sample_prices.csv (example, not committed)
└── volatility_surface.csv (example, not committed)
```

## Adding Data

If you need to add data files:
1. Place them in this directory
2. Ensure they are listed in `.gitignore` if they should not be committed
3. Document the data source and format in this README
