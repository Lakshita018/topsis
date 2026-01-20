# Topsis-Lakshita-102303505

[![PyPI version](https://img.shields.io/pypi/v/Topsis-Lakshita-102303505.svg)](https://pypi.org/project/Topsis-Lakshita-102303505/)
[![Python 3.7+](https://img.shields.io/badge/python-3.7+-blue.svg)](https://www.python.org/downloads/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Implementation of the TOPSIS multi-criteria decision-making method: includes CLI program, Python package, and web service with email functionality.

## What is TOPSIS?

TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution) is a multi-criteria decision analysis method that identifies the alternative closest to the ideal solution and farthest from the negative-ideal solution.

## Repository Structure

This repository contains three implementations:

1. **Part-I: Command Line TOPSIS Program** (`topsis-cli/`)
2. **Part-II: Python Package (PyPI)** (`topsis-python_package/`)
3. **Part-III: TOPSIS Web Service** (`topsis-website/`)

---

## Part-I: Command Line TOPSIS Program

Standalone Python script for running TOPSIS analysis from the command line.

### Location
```
topsis-cli/
├── code.py
├── data.xlsx
└── output.csv
```

### Requirements
```bash
pip install pandas numpy openpyxl
```

### Usage
```bash
python code.py <InputDataFile> <Weights> <Impacts> <OutputResultFileName>
```

### Example
```bash
python code.py data.xlsx "1,1,1,2" "+,+,-,+" output.csv
```

### Error Handling
- Wrong number of parameters
- File not found
- Non-numeric values in criteria columns
- Weights/Impacts count mismatch
- Impacts must be + or -
- Minimum 3 columns required

---

## Part-II: Python Package (PyPI)

Package name: `Topsis-Lakshita-102303505`

Package link: [https://pypi.org/project/Topsis-Lakshita-102303505/](https://pypi.org/project/Topsis-Lakshita-102303505/)

### Installation
```bash
pip install Topsis-Lakshita-102303505
```

### Command Line Usage
```bash
topsis <InputDataFile> <Weights> <Impacts> <OutputResultFileName>
```

### Command Line Examples
```bash
# Equal weights, all positive impacts
topsis data.csv "1,1,1,1,1" "+,+,+,+,+" output.csv

# Different weights, mixed impacts
topsis data.csv "2,1,3,1,2" "+,+,-,+,+" results.csv

# Using Excel file
topsis data.xlsx "1,1,1,2" "+,+,-,+" output.csv
```

### Python API
```python
from Topsis_Lakshita_102303505 import topsis_analysis

result_df = topsis_analysis(
    input_file='data.csv',
    weights='1,1,1,2',
    impacts='+,+,-,+',
    output_file='output.csv'
)

print(result_df)
```

### Features
- Command-line interface after installation
- Python API for programmatic use
- Supports CSV and Excel files
- Comprehensive error handling
- Returns pandas DataFrame
- Generates output CSV file

### Dependencies
- pandas >= 1.0.0
- numpy >= 1.18.0
- openpyxl >= 3.0.0

---

## Part-III: TOPSIS Web Service

Modern web application for TOPSIS analysis with email delivery and results download.

### Live Demo
Vercel Link: [https://topsis-website-alpha.vercel.app/](https://topsis-website-alpha.vercel.app/)

### User Provides
- CSV/Excel file (drag-and-drop or file picker)
- Weights (comma-separated numeric values)
- Impacts (comma-separated + or -)
- Email ID

### Validations
- Number of weights = number of impacts = number of criteria
- Impacts must be + or -
- Correct email format
- All criteria values must be numeric
- Minimum 3 columns required

### Features
- Real-time input validation
- Browser-based TOPSIS calculation
- Results emailed as CSV
- Download results as CSV
- Modern, responsive UI
- Loading indicators during processing

### Technologies
- HTML5, CSS3, JavaScript (ES6+)
- XLSX.js for Excel parsing
- EmailJS for email delivery
- Vercel for deployment

---

## Input File Format

All implementations require the same format:

```csv
Model,Price,Storage,Camera,Looks
M1,250,16,12,5
M2,200,16,8,3
M3,300,32,16,4
```

**Requirements:**
- First column: Alternative names (text)
- Remaining columns: Numeric criteria values
- Minimum 3 columns (1 name + 2 criteria)
- First row contains headers

## Output Format

All implementations produce:

```csv
Model,Price,Storage,Camera,Looks,Topsis Score,Rank
M3,300,32,16,4,0.6910,1
M1,250,16,12,5,0.5347,2
M2,200,16,8,3,0.3082,3
```

**Output includes:**
- All original columns
- Topsis Score (0-1 range, higher is better)
- Rank (1 = best alternative)

## Algorithm Steps

1. Normalize decision matrix using vector normalization
2. Apply weights to normalized values
3. Calculate ideal best and worst solutions
4. Compute Euclidean distances from ideal solutions
5. Calculate performance scores
6. Rank alternatives based on scores


## Algorithm Steps

1. Normalize decision matrix using vector normalization
2. Apply weights to normalized values
3. Calculate ideal best and worst solutions
4. Compute Euclidean distances from ideal solutions
5. Calculate performance scores
6. Rank alternatives based on scores

---

## Links

- **PyPI Package**: [https://pypi.org/project/Topsis-Lakshita-102303505/](https://pypi.org/project/Topsis-Lakshita-102303505/)
- **GitHub Repository**: [https://github.com/Lakshita018/topsis](https://github.com/Lakshita018/topsis)
- **Live Web Application**: [https://topsis-website-alpha.vercel.app/](https://topsis-website-alpha.vercel.app/)

## Author

**Lakshita Gupta**  
Roll Number: 102303505  
Email: lakshitagupta0518@gmail.com

## License

MIT License - Free to use and modify


