# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Overview

This is a numerical methods project focused on polynomial interpolation and approximation of special mathematical functions, specifically the sine integral function Si(x). The project is implemented entirely in a Jupyter notebook with Russian-language documentation and commentary.

## Development Environment

- **Python Version**: 3.13+
- **Package Manager**: uv (modern Python package manager)
- **Main Dependencies**:
  - `matplotlib` - for plotting graphs
  - `pandas` - for tabular data representation
  - `notebook` - Jupyter notebook environment

## Running the Project

### Setting up the environment
```bash
# Activate virtual environment (if not already activated)
.venv\Scripts\activate  # Windows
source .venv/bin/activate  # Unix/Mac

# Install dependencies using uv
uv pip install -e .
```

### Working with the notebook
```bash
# Start Jupyter notebook server
jupyter notebook

# The main notebook is: interpolation_polynomial.ipynb
```

## Code Architecture

### Main Notebook Structure (interpolation_polynomial.ipynb)

The notebook follows a structured mathematical workflow:

1. **Series Computation** - Implements the Taylor series for Si(x):
   - `ratio_series(x, n)` - Computes ratio of consecutive series terms for optimization
   - `series(x, eps)` - Calculates Si(x) using optimized series summation with epsilon precision

2. **Tabulation Functions**:
   - `get_tab_x(a, b, n)` - Creates uniform grid points on interval [a, b] with n intervals
   - `get_tab_x_cheb(a, b, n)` - Creates Chebyshev nodes for optimal interpolation

3. **Interpolation**:
   - `lagrange_polynomial(x, points)` - Implements Lagrange interpolation polynomial
   - Uses `Point` dataclass to store (x, y) coordinate pairs

4. **Analysis Pipeline**:
   - Compares uniform vs Chebyshev node distributions
   - Generates error analysis plots showing interpolation accuracy vs number of nodes
   - Demonstrates Runge phenomenon with uniform nodes and its mitigation with Chebyshev nodes

### Key Implementation Details

- **Numerical Precision**: Default epsilon is 10^-6 for series convergence
- **Default Interval**: [0, 4] for Si(x) computation
- **Error Computation**: Uses absolute difference between series sum and interpolation polynomial
- **Optimization Strategy**: Avoids recalculating factorials by using term ratios in series summation

## Mathematical Background

The project implements approximation of the sine integral:
$$\text{Si}(x) = \int_0^x \frac{\sin t}{t} dt$$

Using Taylor series expansion:
$$\text{Si}(x) = \sum_{n=0}^{\infty} \frac{(-1)^n x^{2n+1}}{(2n+1)(2n+1)!}$$

The key innovation is deriving the ratio formula to compute terms iteratively:
$$q_n(x) = -\frac{x^2 (2n+1)}{(2n+2)(2n+3)^2}$$

This allows computing $a_{n+1} = q_n(x) \cdot a_n$ without recalculating factorials.

## Git Workflow

The repository uses Russian commit messages. Recent commits show focus on:
- Fixing interpolation algorithms
- Adjusting plot intervals
- Completing documentation and bibliography

Main branch is `main` (no separate development branches currently in use).

## Language Note

All code comments, documentation within the notebook, markdown cells, and output labels are in Russian. Variable names and function names are in English for code readability.
