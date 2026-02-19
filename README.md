# Tax Calculation System Requirements

<p style="color:red;">Important: The program is hypothetical, and the numbers are just for debugging purposes. </p>

## Functional Requirements

### Tax Calculation
- The system must calculate federal and state taxes for individuals based on:
    - income
    - deductible expenses
        - Mortgage
        - Student loan
        - Medical expenses
    - filing status
        - individual
        - joint

### Federal Tax Calculation
- Calculates federal tax using progressive tax brackets that vary by filing status.
    - **Individual**
      - 0 to $10,000: 10%
      - $10,001 to $40,000: 12%
      - $40,001 to $100,000: 22%
      - $100,001 to $200,000: 24%
      - $200,001 and above: 32%
    - **Joint**
      - 0 to $20,000: 10%
      - $20,001 to $80,000: 12%
      - $80,001 to $200,000: 22%
      - $200,001 to $400,000: 24%
      - $400,001 and above: 32%

### State Tax Calculation (Massachusetts)
- State tax for Massachusetts is flat rate of 5%.
- Uses the same deductions as federal tax.
- Apply the flat tax rate to the taxable income.


### Deduction Calculation (Both State and Federal)
- There is always a $10000 base deduction amount (regardless of any income), in any type of filing and both in state and federal tax.
- Calculates deductions based on filing status and expenses (mortgage, student loan, medical).
- Additional $5000 deduction for "joint" filers on top of the base deduction amount.



### Input Validation
- Validates inputs for income (should be float), filing status (individual, joint), and deductions to ensure they are correct and within valid ranges.

- Assumes all deductions (mortgage, student loan, medical expenses) are numeric values directly subtracted from income.

### Output Validation
- We don't have negative taxes, if the number is negative, convert it into 0.
- The output should look like: 
    - Federal Tax Owed: $nn.nn
    - State Tax Owed: $nn.nn

### Examples of correct calculations (test cases):
- t1: input: {income: 60000, filingStatus: "Individual", mortgage:0, studentLoad:0, medicalExpenses:0} => output {federalTax: 6799.66, stateTax:2500}

- t2: input: {income: 1000000, filingStatus: "Joint", mortgage:0, studentLoad:0, medicalExpenses:0} => output {federalTax: 270799.10, stateTax:49250.00}

- t3: input: {income: 300000, filingStatus: "Individual", mortgage:0, studentLoad:10000, medicalExpenses:0} => output {federalTax: 67400.00, stateTax:14000.00}

- t4: input: {income: 300000, filingStatus: "Joint", mortgage:0, studentLoad:1000, medicalExpenses:0} => output {federalTax: 55759.42, stateTax:14200.00}

- t5: input: {income: 200, filingStatus: "Individual", mortgage:0, studentLoad:0, medicalExpenses:0} => output {federalTax: 0, stateTax:0}
- t6: input: {income: 200, filingStatus: "Joint", mortgage:0, studentLoad:0, medicalExpenses:0} => output {federalTax: 0, stateTax:0}

- t7: input: {income: 85000, filingStatus: "Joint", mortgage:0, studentLoad:0, medicalExpenses:10000} => output {federalTax: 6799.88, stateTax:3000.00}

- t8: input: {income: 85000, filingStatus: "Individual", mortgage:0, studentLoad:0, medicalExpenses:10000} => output {federalTax: 10099.66, stateTax:3250.00}

- t9: input: {income: 0, filingStatus: "Joint", mortgage:0, studentLoad:10000, medicalExpenses:10000} => output {federalTax: 0, stateTax:0}

- t10: input: {income: 0, filingStatus: "Individual", mortgage:0, studentLoad:10000, medicalExpenses:10000} => output {federalTax: 0, stateTax:0}
