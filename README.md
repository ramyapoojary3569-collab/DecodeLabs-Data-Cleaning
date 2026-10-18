import pandas as pd
import numpy as np
from pathlib import Path

# 1. Open the Excel dataset
file_path = Path.home() / "Desktop" / "DecodeLabs_Project1" / "Dataset for Data Analytics.xlsx"

df = pd.read_excel(file_path)

print("Original Dataset:")
print(df.head())

# 2. Check dataset information
print("\nDataset Shape:", df.shape)
print("\nMissing Values:")
print(df.isnull().sum())

# 3. Remove duplicate rows
df = df.drop_duplicates()

# 4. Clean column names
df.columns = df.columns.str.strip()

# 5. Handle missing coupon codes
if "CouponCode" in df.columns:
    df["CouponCode"] = df["CouponCode"].fillna("No Coupon")

# 6. Save cleaned dataset
output_path = file_path.parent / "Cleaned_Data.xlsx"
df.to_excel(output_path, index=False)

print("\nCleaning completed successfully!")
print("Cleaned file saved at:", output_path)
