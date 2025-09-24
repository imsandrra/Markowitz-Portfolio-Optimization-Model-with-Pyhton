# Markowitz Portfolio Optimization Model

[![Python 3.9+](https://img.shields.io/badge/python-3.9+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

## Overview

This repository implements Modern Portfolio Theory (MPT) optimization for constructing efficient portfolios across six major stocks representing different market sectors.

**Research Period:** January 2020 - August 2025  
**Assets:** AAPL, NVDA, PG, JNJ, GS, XOM  
**Methodology:** Mean-Variance Optimization (Markowitz Model)

## Key Results

- **Minimum Variance Portfolio:** 17.5% volatility, 17.3% annual return
- **Optimal Sharpe Ratio:** ~1.42 at 22.3%-27.3% volatility range
- **Dominant Strategy:** Defensive asset allocation (PG: 35.6%, JNJ: 45.5%)

## Quick Start

### Installation
```bash
# Clone repository
git clone https://github.com/yourusername/markowitz-portfolio.git
cd markowitz-portfolio

# Create virtual environment
python -m venv venv
source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt
