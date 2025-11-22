Amazon Sales Data Analysis (Python + Pandas)

This project analyzes a raw Amazon sales log taken from Kaggle.
The goal was to work with real-world messy data — including inconsistent price formats, missing values, string-based percentage fields, and noisy category information — and extract meaningful product and category insights using Python and Pandas.

The focus is on data cleaning, preparation, segmentation, and business-focused metrics.

  *** Key Features of the Analysis ***
   
( 1. Price Cleaning & Transformation )
    
Removed ₹ symbols and commas

Stripped whitespace

Converted string prices to numeric types

Dropped invalid and zero-value prices



( 2. Product-Level Metrics )

Calculated:

Total Revenue per product

Units Sold

Average Selling Price (ASP)

Top Products by Revenue



( 3. Category-Level Insights )

Identified:

Categories with highest revenue

Average discount % per category

Count of products priced above category average



( 4. Discount Analysis )

Cleaned and converted discount_percentage

Computed Top Products by Average Discount %



----🛠️ Tech Stack----

Python

Pandas

NumPy

PyCharm ,  Python Script



📁 Project Structure
amazon-sales-analysis/
│
├── amazon_analysis.ipynb      # (or analysis.py) main analysis code
├── README.md                  # project documentation
└── data/                      # dataset reference (dataset not included due to Kaggle license)



----- Dataset Source ------

This analysis is based on the public Kaggle dataset:

Amazon Sales Dataset — Raw Purchase Logs
(Users must download the dataset directly from Kaggle due to licensing rules.)



📈 Sample Insights

Products with the highest revenue

Categories contributing most to total sales

Highest discounted products

Distribution of product prices

Products performing above category price averages



 -------- What This Project Demonstrates--------

This project shows practical, real-world skills in:

Cleaning messy e-commerce transactional data

Feature engineering and segmentation

Grouping, aggregating, and deriving KPIs

Working with imperfect data

Structuring an analysis pipeline





***** Future Enhancements *****

Potential next steps:

Visualizations (Matplotlib/Seaborn)

Outlier analysis using IQR

Price elasticity estimation

Product similarity mapping

Customer clustering (if customer IDs exist)

👤 Author

Mithun (Mob)
Aspiring Data Analyst • Python • SQL • Pandas • Problem Solver
