# TOPSIS Implementation Suite

A comprehensive TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution) implementation with three different interfaces for multi-criteria decision analysis.

## Overview

TOPSIS is a multi-criteria decision analysis method that identifies the alternative closest to the ideal solution and farthest from the negative-ideal solution. This repository contains three different implementations:

1. **topsis-cli** - Command-line interface for local analysis
2. **topsis-python_package** - Installable Python package published on PyPI
3. **topsis-website** - Web-based interface with email delivery

## What is TOPSIS?

TOPSIS helps in making decisions when multiple criteria need to be considered simultaneously. The algorithm:
- Normalizes the decision matrix
- Applies weights to criteria
- Identifies ideal best and worst solutions
- Calculates distances from ideal solutions
- Computes performance scores
- Ranks alternatives based on scores

## Part 1: TOPSIS-CLI

A standalone Python script for running TOPSIS analysis from the command line.

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

### Examples
```bash
# Equal weights, all positive impacts
python code.py data.xlsx "1,1,1,1,1" "+,+,+,+,+" output.csv

# Different weights, mixed impacts
python code.py data.csv "2,1,3,1,2" "+,+,-,+,+" results.csv
```

### Features
- Supports CSV and Excel files
- Vector normalization of decision matrix
- Weighted matrix calculation
- Ideal best and worst solutions
- Euclidean distance computation
- Performance score calculation
- Ranking of alternatives
- Detailed console output with formatted results

### Input File Format
- First column: Alternative names (text)
- Remaining columns: Numeric criteria values
- Minimum 3 columns required
- Headers in first row

### Output
Creates a CSV file with:
- All original columns
- Topsis Score (0-1 range, higher is better)
- Rank (1 = best alternative)

### Error Handling
- File existence validation
- Column count verification
- Numeric value checking
- Parameter count matching
- Impact sign validation

## Part 2: TOPSIS-Python_Package

A professionally packaged Python library available on PyPI for easy installation and use in any Python project.

### Location
```
topsis-python_package/
├── Topsis_Lakshita_102303505/
│   ├── __init__.py
│   ├── __main__.py
│   └── topsis.py
├── setup.py
├── pyproject.toml
├── LICENSE
└── MANIFEST.in
```

### Installation
```bash
pip install Topsis-Lakshita-102303505
```

### Command Line Usage
```bash
topsis <InputDataFile> <Weights> <Impacts> <OutputResultFileName>
```

### Python API Usage
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
- Published on PyPI for global distribution
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

### Package Structure
- Entry point for command-line usage
- Importable module for Python scripts
- Proper package metadata
- MIT License
- Comprehensive documentation

## Part 3: TOPSIS-Website

A modern web application for TOPSIS analysis with email delivery and results download functionality.

### Location
```
topsis-website/
├── index.html
├── styles.css
├── app.js
├── sample-data.csv
└── vercel.json
```

### Features
- Upload CSV or Excel files via drag-and-drop or file picker
- Real-time input validation
- Browser-based TOPSIS calculation
- Email results to specified address
- Download results as CSV
- Modern, responsive UI with gradient design
- Error and success message displays
- Loading indicators during processing

### Technologies
- HTML5 for structure
- CSS3 for styling with animations
- JavaScript (ES6+) for TOPSIS implementation
- XLSX.js for Excel file parsing
- EmailJS for email delivery
- Vercel for hosting

### Setup Instructions

#### EmailJS Configuration
1. Create account at https://www.emailjs.com/
2. Add email service (Gmail, Outlook, etc.)
3. Create email template with variables:
   - to_email
   - file_name
   - results
4. Get credentials:
   - Public Key
   - Service ID
   - Template ID
5. Update app.js line 4 with Public Key
6. Update app.js line 322 with Service ID and Template ID

#### Local Testing
```bash
# Using Python
python -m http.server 8000

# Using Node.js
npx http-server
```

#### Deployment to Vercel
```bash
npm install -g vercel
cd topsis-website
vercel
```

### Usage Workflow
1. Upload CSV or XLSX file
2. Enter comma-separated weights (e.g., "1,1,1,2")
3. Enter comma-separated impacts (e.g., "+,+,-,+")
4. Enter valid email address
5. Click "Analyze & Send Results"
6. View results preview in browser
7. Check email for formatted results table
8. Download results as CSV if needed

### Validation Rules
- Number of weights must equal number of impacts
- Number of weights must equal number of criteria columns
- Weights must be numeric values
- Impacts must be + or - only
- Email must be valid format
- All criteria values must be numeric
- Minimum 3 columns required

### Algorithm Implementation
- Client-side JavaScript implementation
- No server-side processing required
- Real-time calculation
- Supports large datasets
- Memory-efficient processing

## Common Parameters

### Weights
Comma-separated numeric values representing the importance of each criterion.
- Example: "1,1,1,2" means 4 criteria with last one twice as important
- Must match the number of criteria columns
- Can be integers or decimals

### Impacts
Comma-separated + or - signs indicating beneficial or cost criteria.
- "+" for beneficial criteria (higher values are better)
- "-" for cost criteria (lower values are better)
- Example: "+,+,-,+" means first two and last are beneficial, third is cost
- Must match the number of criteria columns

## Input Data Format

All three implementations require the same input format:

```
Model,Price,Storage,Camera,Looks
M1,250,16,12,5
M2,200,16,8,3
M3,300,32,16,4
M4,275,32,8,4
M5,225,16,16,2
```

Requirements:
- Minimum 3 columns (1 identifier + 2 criteria)
- First column contains alternative names
- Remaining columns contain numeric values only
- First row contains headers
- CSV or XLSX format supported

## Output Format

All implementations produce similar output:

```
Model,Price,Storage,Camera,Looks,Topsis Score,Rank
M3,300,32,16,4,0.6910,1
M1,250,16,12,5,0.5347,2
M4,275,32,8,4,0.5144,3
M5,225,16,16,2,0.4013,4
M2,200,16,8,3,0.3082,5
```

Output includes:
- All original columns preserved
- Topsis Score: Performance score (0-1 range)
- Rank: Integer ranking (1 = best)

## TOPSIS Algorithm Steps

1. **Normalize Decision Matrix**
   - Vector normalization: each value divided by square root of sum of squares
   
2. **Apply Weights**
   - Multiply normalized values by corresponding weights
   
3. **Calculate Ideal Solutions**
   - Ideal Best: Max for beneficial (+), Min for cost (-)
   - Ideal Worst: Min for beneficial (+), Max for cost (-)
   
4. **Calculate Euclidean Distances**
   - Distance from each alternative to ideal best
   - Distance from each alternative to ideal worst
   
5. **Compute Performance Scores**
   - Score = Distance to worst / (Distance to best + Distance to worst)
   
6. **Rank Alternatives**
   - Sort by score in descending order
   - Assign ranks (1 = best)

## Error Handling

All implementations include comprehensive error handling:

- File existence verification
- File format validation
- Column count checking
- Numeric value validation
- Parameter count matching
- Weight format validation
- Impact sign validation
- Email format validation (web version)

## Use Cases

### CLI Version Best For:
- Quick local analysis
- Batch processing
- Script automation
- No internet required

### Python Package Best For:
- Integration into larger Python projects
- Reproducible research
- Data analysis pipelines
- Jupyter notebooks

### Web Version Best For:
- Non-technical users
- Quick analysis without installation
- Sharing results via email
- Cross-platform compatibility
- Mobile devices

## Author

Lakshita Gupta
Roll Number: 102303505
Email: lakshitagupta0518@gmail.com

## License

MIT License - Free to use and modify

## Links

- PyPI Package: https://pypi.org/project/Topsis-Lakshita-102303505/
- GitHub Repository: https://github.com/Lakshita018/topsis

## Version

1.0.0 (2026-01-20)
- Initial release
- Three different implementations
- CSV and Excel support
- Comprehensive documentation
- Error handling and validation
