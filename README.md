# Olist E-Commerce Funnel Analysis 🇧🇷

## Overview
This project performs a comprehensive **Product Analytics** audit on the [Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce). It constructs and visualizes two critical business funnels—**Seller Acquisition** and **Order Fulfillment**—to identify operational bottlenecks and conversion leaks.

The core feature is a custom **Sankey Pipe Diagram** that visualizes user flow and explicitly magnifies "drop-off" points, allowing stakeholders to instantly spot high-friction stages in the pipeline.

## Key Features
* **Marketing Funnel Analysis**: Tracks the conversion of Marketing Qualified Leads (MQLs) $\rightarrow$ Closed Deals $\rightarrow$ Active Sellers.
* **Order Fulfillment Funnel**: audits the operational health from Order Placed $\rightarrow$ Payment Approved $\rightarrow$ Shipped $\rightarrow$ Delivered.
* **Sensitivity Visualization**: Includes a specialized `plot_sankey_pipe` function that **magnifies drop-off flows by 10x**, making even small efficiency losses visible for executive review.
* **Interactive Plotly Charts**: Generates dynamic HTML-based visualizations.

## Prerequisites
* Python 3.7+
* Pandas
* Plotly

```bash
pip install pandas plotly
```

## Dataset Structure
This project requires the Olist dataset CSVs. Ensure the following files are available in your directory (or update paths in the script):
* `olist_marketing_qualified_leads_dataset.csv`
* `olist_closed_deals_dataset.csv`
* `olist_orders_dataset.csv`
* `olist_order_items_dataset.csv`

## Quick Start

### 1. Load Data
```python
import pandas as pd

# Load your datasets
mql = pd.read_csv('path/to/olist_marketing_qualified_leads_dataset.csv')
closed = pd.read_csv('path/to/olist_closed_deals_dataset.csv')
items = pd.read_csv('path/to/olist_order_items_dataset.csv')
orders = pd.read_csv('path/to/olist_orders_dataset.csv')
```

### 2. Initialize Analyzer
```python
from funnel_analyzer import OlistFunnelAnalyzer

analyzer = OlistFunnelAnalyzer(
    marketing_qualified_leads=mql,
    closed_deals=closed,
    order_items=items,
    orders=orders
)
```

### 3. Generate Visualizations
```python
# Build the Order Data
order_data = analyzer.build_order_funnel()

# Option A: Executive Summary (Standard Horizontal Funnel)
analyzer.plot_horizontal_funnel(order_data, "Order Fulfillment (Executive View)")

# Option B: Diagnostic View (Sankey with Magnified Drop-offs)
# Useful for finding operational leaks
analyzer.plot_sankey_pipe(order_data, "Order Fulfillment Flow & Dropoffs")
```

## Methodology

### The "Magnified Drop-off" Logic
In standard Sankey diagrams, small drop-off percentages (e.g., 1-2%) are often invisible. This tool applies a **10x scaling factor** specifically to "Lost" flows.
* **Why?** In high-volume businesses like Olist (100k+ orders), a 1% drop in "Payment Approval" represents significant revenue loss. The visualization forces this to be visually dominant to prompt investigation.

## Project Structure
```text
├── funnel_analyzer.py    # Main class containing logic and plotting functions
├── main.py               # Usage script to load data and run analysis
├── README.md             # Project documentation
└── data/                 # Directory for Olist CSV files
```

## License
This project is open-source and available under the MIT License. Data provided by Olist via Kaggle.
