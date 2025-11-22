import pandas as pd

# Display full columns
pd.set_option('display.max_columns', None)
pd.set_option('display.width', None)

# Load dataset
df = pd.read_csv("E:/MITHUN FILES/workshop/amazon.csv")

# ---------------------------
#  CLEANING price columns
# ---------------------------

# Clean discounted_price
df["discounted_price"] = (
    df["discounted_price"]
    .str.replace("₹", "", regex=False)
    .str.replace(",", "", regex=False)
    .str.strip()
    .astype(float)
)

# Remove rows where discounted price is invalid
df = df.dropna(subset=["discounted_price"])

# Remove zero / negative prices if any
df = df[df["discounted_price"] > 0]

# ---------------------------
#  TOP PRODUCTS by revenue
# ---------------------------

product_revenue = (
    df.groupby("product_name")["discounted_price"]
      .sum()
      .reset_index()
      .sort_values("discounted_price", ascending=False)
)

print("\nTop 10 products by revenue:")
print(product_revenue.head(10))


# ---------------------------
#  PRODUCT STATS (Revenue, Units Sold, Avg Price)
# ---------------------------

product_stats = (
    df.groupby("product_name")
      .agg(
          total_revenue=("discounted_price", "sum"),
          units_sold=("discounted_price", "count"),
          avg_price=("discounted_price", "mean")
      )
      .reset_index()
      .sort_values("total_revenue", ascending=False)
)

print("\nProduct Stats:")
print(product_stats.head(10))


# ---------------------------
#  TOP CATEGORIES by revenue
# ---------------------------

category_disc = (
    df.groupby("category")["discounted_price"]
      .sum()
      .reset_index()
      .rename(columns={"discounted_price": "total_revenue"})
      .sort_values("total_revenue", ascending=False)
)

print("\nTop categories by revenue:")
print(category_disc.head(10))


# ---------------------------
#  CLEAN discount_percentage
# ---------------------------

df["discount_percentage"] = (
    df["discount_percentage"]
    .str.replace("%", "", regex=False)
    .str.strip()
    .astype(float)
)


# ---------------------------
#  Top products by AVG discount %
# ---------------------------

large_disc = (
    df.groupby("product_name")["discount_percentage"]
      .mean()                 # FIXED: avg, not sum
      .reset_index()
      .sort_values("discount_percentage", ascending=False)
)

print("\nTop products by discount %:")
print(large_disc.head(10))


# ---------------------------
#  Average discount % per category
# ---------------------------

avg_disc = (
    df.groupby("category")["discount_percentage"]
      .mean()
      .reset_index()
      .sort_values("discount_percentage", ascending=False)
)

print("\nAvg discount % per category:")
print(avg_disc.head(10))


# ---------------------------
#  Products priced above category avg
# ---------------------------

# Category avg price
avg_price_category = df.groupby("category")["discounted_price"].mean()

# Map back to rows
df["avg_price_category"] = df["category"].map(avg_price_category)

# Count products above avg, per category
count_above_per_cat = (
    (df["discounted_price"] > df["avg_price_category"])
    .groupby(df["category"])
    .sum()
)

print("\nCount of above-average priced products per category:")
print(count_above_per_cat)

