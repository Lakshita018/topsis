# TOPSIS Package - Complete User Manual

## Table of Contents
1. [Package Overview](#package-overview)
2. [Installation](#installation)
3. [Quick Start](#quick-start)
4. [Detailed Usage](#detailed-usage)
5. [Input File Requirements](#input-file-requirements)
6. [Parameters Explained](#parameters-explained)
7. [Output Format](#output-format)
8. [Error Messages & Solutions](#error-messages--solutions)
9. [Examples](#examples)
10. [Python API Usage](#python-api-usage)
11. [Troubleshooting](#troubleshooting)

---

## Package Overview

**Package Name**: Topsis-YourName-RollNumber  
**Version**: 1.0.0  
**Purpose**: Multi-criteria decision analysis using TOPSIS method  
**PyPI Link**: https://pypi.org/project/Topsis-YourName-RollNumber/

### What is TOPSIS?

TOPSIS (Technique for Order of Preference by Similarity to Ideal Solution) is a multi-criteria decision making method that:
- Identifies the best alternative from a set of alternatives
- Based on multiple evaluation criteria
- Considers both beneficial and non-beneficial criteria
- Ranks alternatives from best to worst

### How TOPSIS Works

1. **Normalize** the decision matrix
2. **Apply weights** to criteria
3. **Identify ideal solutions** (best and worst)
4. **Calculate distances** from ideal solutions
5. **Compute performance scores**
6. **Rank alternatives** based on scores

---

## Installation

### Requirements
- Python 3.7 or higher
- pip (Python package installer)

### Install from PyPI

```bash
pip install Topsis-YourName-RollNumber
```

### Install from Source

```bash
# Clone or download the repository
cd path/to/topsis
pip install -e .
```

### Verify Installation

```bash
python -c "import Topsis_YourName_RollNumber; print(Topsis_YourName_RollNumber.__version__)"
```

---

## Quick Start

### Command Line Usage

```bash
topsis <InputDataFile> <Weights> <Impacts> <OutputResultFileName>
```

### Quick Example

```bash
# Download or create a sample data file
topsis data.csv "1,1,1,2" "+,+,-,+" results.csv
```

---

## Detailed Usage

### Method 1: Using Installed Command

After installation, use the `topsis` command directly:

```bash
topsis input.csv "1,1,1,1" "+,+,+,+" output.csv
```

### Method 2: Using Python Module

```bash
python -m Topsis_YourName_RollNumber input.xlsx "2,1,3" "+,-,+" output.csv
```

### Method 3: In Python Script

```python
from Topsis_YourName_RollNumber import topsis_analysis

result_df = topsis_analysis(
    input_file='data.csv',
    weights='1,1,1,2',
    impacts='+,+,-,+',
    output_file='output.csv'
)

print(result_df)
```

---

## Input File Requirements

### File Format
- **Supported formats**: CSV (.csv) or Excel (.xlsx)
- **Minimum columns**: 3 (1 name column + 2 criteria columns)

### Structure

| Column 1 (Name) | Column 2 (Criterion 1) | Column 3 (Criterion 2) | ... |
|-----------------|------------------------|------------------------|-----|
| Alternative 1   | Numeric value          | Numeric value          | ... |
| Alternative 2   | Numeric value          | Numeric value          | ... |

### Rules
✅ First column: Alternative names (text)  
✅ Columns 2 onwards: Numeric criteria values only  
❌ No missing values in criteria columns  
❌ No non-numeric values in criteria columns

### Example CSV File

```csv
Fund Name,Price,Storage,Camera,Looks
M1,250,16,12,5
M2,200,16,8,3
M3,300,32,16,4
M4,275,32,8,4
M5,225,16,16,2
```

### Example Excel File

Create an Excel file with the same structure as above.

---

## Parameters Explained

### 1. InputDataFile
- **Type**: String (file path)
- **Format**: CSV or Excel (.xlsx)
- **Example**: `"data.csv"`, `"C:/Users/data.xlsx"`

### 2. Weights
- **Type**: String (comma-separated numeric values)
- **Purpose**: Relative importance of each criterion
- **Format**: `"w1,w2,w3,...,wn"`
- **Example**: `"1,1,1,2"` (4 criteria, last one is twice as important)
- **Rules**:
  - Must match the number of criteria columns
  - All values must be numeric (integers or decimals)
  - No spaces (or use quotes if spaces exist)

### 3. Impacts
- **Type**: String (comma-separated + or - signs)
- **Purpose**: Define if higher is better (+) or lower is better (-)
- **Format**: `"+,-,+,...,+"`
- **Example**: `"+,+,-,+"` 
  - `+` for beneficial criteria (profit, quality, efficiency)
  - `-` for cost criteria (price, defects, time)
- **Rules**:
  - Must match the number of criteria columns
  - Only `+` or `-` allowed
  - No spaces between commas

### 4. OutputResultFileName
- **Type**: String (file path)
- **Format**: CSV file
- **Example**: `"results.csv"`, `"output/analysis_results.csv"`
- **Note**: Directory must exist; file will be created/overwritten

---

## Output Format

### Output CSV Structure

The output file contains all original columns plus:
- **Topsis Score**: Performance score (range: 0 to 1, higher is better)
- **Rank**: Integer rank (1 = best alternative)

### Example Output

```csv
Fund Name,Price,Storage,Camera,Looks,Topsis Score,Rank
M3,300,32,16,4,0.691,1
M1,250,16,12,5,0.534,2
M2,200,16,8,3,0.308,3
```

### Terminal Output

The program also displays formatted results in the terminal:

```
================================================================================
TOPSIS ANALYSIS COMPLETED SUCCESSFULLY
================================================================================

Input File: data.csv
Weights: [1.0, 1.0, 1.0, 2.0]
Impacts: ['+', '+', '-', '+']
Output File: results.csv

--------------------------------------------------------------------------------
RESULTS:
--------------------------------------------------------------------------------
Fund Name  Price  Storage  Camera  Looks  Topsis Score  Rank
       M3    300       32      16      4      0.691234     1
       M1    250       16      12      5      0.534156     2
       M2    200       16       8      3      0.308245     3
================================================================================
```

---

## Error Messages & Solutions

### Error 1: Incorrect Number of Parameters
```
Error: Incorrect number of parameters.
```
**Solution**: Provide exactly 4 arguments:
```bash
topsis input.csv "1,1,1" "+,+,+" output.csv
```

### Error 2: File Not Found
```
Error: Input file not found.
```
**Solution**: 
- Check file path is correct
- Use absolute path if needed
- Ensure file exists in the specified location

### Error 3: Insufficient Columns
```
Error: Input file must contain at least three columns.
```
**Solution**: Add more columns (minimum 1 name + 2 criteria)

### Error 4: Non-Numeric Values
```
Error: From 2nd to last columns must contain numeric values only.
```
**Solution**: 
- Remove text from criteria columns
- Replace missing values with numbers
- Check for special characters

### Error 5: Mismatched Weights
```
Error: Number of weights must match number of criteria.
```
**Solution**: 
If you have 5 criteria columns, provide 5 weights:
```bash
topsis data.csv "1,1,1,1,1" "+,+,+,+,+" output.csv
```

### Error 6: Mismatched Impacts
```
Error: Number of impacts must match number of criteria.
```
**Solution**: 
If you have 4 criteria, provide 4 impacts:
```bash
topsis data.csv "1,1,1,1" "+,+,-,+" output.csv
```

### Error 7: Invalid Impact Values
```
Error: Impacts must be either '+' or '-'.
```
**Solution**: Use only `+` or `-`:
```bash
# Wrong: "+,+,*,+"
# Correct: "+,+,-,+"
```

### Error 8: Format Error
```
Error: Weights and impacts must be comma-separated.
```
**Solution**: Use commas, no spaces:
```bash
# Wrong: "1 1 1 1"
# Correct: "1,1,1,1"
```

---

## Examples

### Example 1: Mobile Phone Selection

**Data File (phones.csv)**:
```csv
Model,Price,Camera,Battery,RAM
Phone A,15000,12,4000,4
Phone B,20000,48,5000,6
Phone C,25000,64,4500,8
Phone D,18000,32,5500,6
```

**Command**:
```bash
topsis phones.csv "2,3,2,1" "-,+,+,+" results.csv
```

**Explanation**:
- Price: Weight=2, Impact=- (lower is better)
- Camera: Weight=3, Impact=+ (higher is better, most important)
- Battery: Weight=2, Impact=+ (higher is better)
- RAM: Weight=1, Impact=+ (higher is better)

---

### Example 2: Supplier Selection

**Data File (suppliers.xlsx)**:
| Supplier | Cost | Quality | Delivery Time | Reliability |
|----------|------|---------|---------------|-------------|
| Supplier A | 1000 | 85 | 5 | 90 |
| Supplier B | 1200 | 95 | 3 | 95 |
| Supplier C | 900  | 75 | 7 | 80 |

**Command**:
```bash
topsis suppliers.xlsx "3,4,2,3" "-,+,-,+" output.csv
```

**Explanation**:
- Cost: Impact=- (lower cost is better)
- Quality: Impact=+ (higher quality is better)
- Delivery Time: Impact=- (faster delivery is better)
- Reliability: Impact=+ (higher reliability is better)

---

### Example 3: Investment Analysis

**Data File (investments.csv)**:
```csv
Investment,ROI,Risk,Liquidity,Growth
Option A,12,7,8,15
Option B,15,9,6,20
Option C,10,5,9,12
Option D,18,8,7,25
```

**Command**:
```bash
topsis investments.csv "4,2,3,3" "+,-,+,+" results.csv
```

---

## Python API Usage

### Basic Usage

```python
from Topsis_YourName_RollNumber import topsis_analysis

# Perform TOPSIS analysis
result = topsis_analysis(
    input_file='data.csv',
    weights='1,1,1,1',
    impacts='+,+,+,+',
    output_file='output.csv'
)

# Display results
print(result)
```

### Advanced Usage with Error Handling

```python
from Topsis_YourName_RollNumber import topsis_analysis

try:
    result_df = topsis_analysis(
        input_file='data.xlsx',
        weights='2,1,3,1',
        impacts='+,+,-,+',
        output_file='results.csv'
    )
    
    # Get top 3 alternatives
    top_3 = result_df.nsmallest(3, 'Rank')
    print("Top 3 Alternatives:")
    print(top_3)
    
    # Get best alternative
    best = result_df.loc[result_df['Rank'] == 1]
    print(f"\nBest Alternative: {best.iloc[0, 0]}")
    
except FileNotFoundError as e:
    print(f"File error: {e}")
except ValueError as e:
    print(f"Validation error: {e}")
```

### Integration in Data Pipeline

```python
import pandas as pd
from Topsis_YourName_RollNumber import topsis_analysis

# Read and preprocess data
df = pd.read_csv('raw_data.csv')

# Clean data
df = df.dropna()

# Save cleaned data
df.to_csv('clean_data.csv', index=False)

# Run TOPSIS
result = topsis_analysis(
    input_file='clean_data.csv',
    weights='1,2,1,3',
    impacts='+,-,+,+',
    output_file='final_ranking.csv'
)

# Further analysis
print(result.describe())
```

---

## Troubleshooting

### Issue: Module not found
**Problem**: `ModuleNotFoundError: No module named 'Topsis_YourName_RollNumber'`

**Solution**:
```bash
pip install Topsis-YourName-RollNumber
# or
pip install --upgrade Topsis-YourName-RollNumber
```

### Issue: Permission denied
**Problem**: Cannot write output file

**Solution**:
- Check write permissions in output directory
- Close the output file if it's open
- Use a different output location

### Issue: Unexpected results
**Problem**: Rankings seem incorrect

**Solution**:
- Verify impact signs (+ vs -)
- Check if weights reflect your priorities
- Ensure data doesn't have outliers
- Review the normalization method

### Issue: Large files slow
**Problem**: Processing takes too long

**Solution**:
- TOPSIS is efficient, but very large datasets may take time
- Consider filtering data first
- Use CSV instead of Excel for faster reading

---

## Additional Resources

- **PyPI Package**: https://pypi.org/project/Topsis-YourName-RollNumber/
- **GitHub Repository**: [Your GitHub URL]
- **TOPSIS Algorithm**: [Wikipedia](https://en.wikipedia.org/wiki/TOPSIS)
- **Issue Tracker**: [Your GitHub Issues URL]

---

## Support

For bugs, questions, or feature requests:
- Open an issue on GitHub
- Email: your.email@example.com

---

## Version History

**v1.0.0** (2026-01-20)
- Initial release
- TOPSIS algorithm implementation
- CSV and Excel support
- Command-line interface
- Python API
- Comprehensive error handling

---

## License

MIT License - See LICENSE file for details

---

**Happy Decision Making with TOPSIS! 🎯**
