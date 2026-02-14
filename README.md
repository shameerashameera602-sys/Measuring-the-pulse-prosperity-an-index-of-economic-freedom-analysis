Python
import pandas as pd
import numpy as np

# Sample data for countries
data = {
    "Country": ["India", "USA", "Germany", "Japan"],
    
    # Prosperity indicators
    "GDP_per_Capita": [2500, 70000, 52000, 49000],
    "Employment_Rate": [45, 60, 58, 59],
    "Life_Expectancy": [70, 79, 81, 84],
    
    # Economic Freedom indicators
    "Business_Freedom": [65, 85, 80, 78],
    "Trade_Freedom": [70, 90, 88, 85],
    "Property_Rights": [55, 92, 90, 89]
}

df = pd.DataFrame(data)
print(df)
Step 1: Normalize the data (0–1 scale)
Copy code
Python
def normalize(column):
    return (column - column.min()) / (column.max() - column.min())

normalized_df = df.copy()

for col in df.columns[1:]:
    normalized_df[col] = normalize(df[col])

print(normalized_df)
Step 2: Prosperity Index Calculation
Copy code
Python
normalized_df["Prosperity_Index"] = (
    normalized_df["GDP_per_Capita"] +
    normalized_df["Employment_Rate"] +
    normalized_df["Life_Expectancy"]
) / 3
Step 3: Economic Freedom Index Calculation
Copy code
Python
normalized_df["Economic_Freedom_Index"] = (
    normalized_df["Business_Freedom"] +
    normalized_df["Trade_Freedom"] +
    normalized_df["Property_Rights"]
) / 3
Step 4: Final Output
Copy code
Python
final_result = normalized_df[[
    "Country",
    "Prosperity_Index",
    "Economic_Freedom_Index"
]]

print(final_result)
