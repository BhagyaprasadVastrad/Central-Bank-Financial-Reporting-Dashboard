
# Dashboard Specification

## Objective
Simulate financial reporting for a central bank. Track monetary supply, currency issuance, interest rates, inflation, GDP growth, bank balances, loan default rates, and regulatory compliance.

## Dataset schema (columns)
- Date (Date)
- Currency_Issued (Numeric, millions)
- Reserve_Ratio (Numeric, %)
- Interest_Rate (Numeric, %)
- Inflation_Rate (Numeric, %)
- GDP_Growth (Numeric, %)
- Bank_Balances (Numeric, millions)
- Loan_Default_Rate (Numeric, %)
- Regulatory_Compliance_Score (Numeric, 0-100)
- Scenario_Type (Text) - Baseline / Stress Test / High Inflation

## Visuals & Aggregations (Letter Page Layout)
Header: Title & subtitle

Left column (40%):
- KPI cards: Total Currency Issued (SUM), Total Bank Balances (SUM), Average Reserve Ratio (AVERAGE), Loan Default Rate (AVERAGE)
- Line chart: Date X-axis, Currency_Issued (SUM) & Bank_Balances (SUM)

Right column (60%):
- Combo chart: Date X-axis, Interest_Rate (AVERAGE) as columns, Inflation_Rate (AVERAGE) as line (secondary axis)
- Gauge: Regulatory_Compliance_Score (AVERAGE)
- Waterfall: Scenario_Type (Category), Currency_Issued (SUM) or Bank_Balances (SUM)

Bottom row (optional):
- Bar chart: GDP_Growth (AVERAGE) by Month
- Table: Date, Loan_Default_Rate (AVG), Compliance (AVG), Currency_Issued (SUM) with conditional formatting for alerts

## Additional suggested visuals
- Area chart: Monetary supply composition (stacked)
- Scatter plot: Inflation vs GDP growth (bubble sized by Interest Rate)
- Heatmap: Compliance & defaults by region/department (if available)
- Bullet chart: Reserve Ratio vs target
- Sparklines for KPI trends

## Sample DAX
TotalCurrencyIssued = SUM('FinancialData'[Currency_Issued])
AvgInterestRate = AVERAGE('FinancialData'[Interest_Rate])
ComplianceStatus = IF(AVERAGE('FinancialData'[Regulatory_Compliance_Score]) < 70, "Alert", "OK")
DefaultChangeMoM =
VAR Prev = CALCULATE(AVERAGE('FinancialData'[Loan_Default_Rate]), PREVIOUSMONTH('FinancialData'[Date]))
RETURN DIVIDE(AVERAGE('FinancialData'[Loan_Default_Rate]) - Prev, Prev)

