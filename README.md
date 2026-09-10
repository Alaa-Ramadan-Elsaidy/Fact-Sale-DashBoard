<!-- HEADER SECTION -->
<div align="center">
  <h1>FactSale Sales Analysis & Dashboard</h1>
  <h3>Voltix Task 2</h3>
  <p>
    <b>Author:</b> Alaa Ayman Ramadan &nbsp;|&nbsp; 
    <b>Supervisor / Entity:</b> Voltix
  </p>
</div>

<hr />

<p>A full data analytics project on the <b>FactSale</b> sales dataset, completed under the guidance and supervision of <b>Voltix</b> (Task 2). The workflow spans cleaning and validating raw data in Python, performing exploratory analysis, and building an interactive <b>Power BI</b> dashboard to answer real business questions and deliver actionable strategic recommendations.</p>

<h2>📌 Project Overview</h2>

<p>The goal of this project was not just to clean data and draw charts, but to go through a full end-to-end data analytics lifecycle:</p>

<ol>
  <li>Understand the raw dataset and its relational structure</li>
  <li>Clean and validate the data (with special attention to date fields, missing values, and business rules)</li>
  <li>Formulate business questions worth answering for executive decision-making</li>
  <li>Build a clean, interactive, and functional Power BI dashboard</li>
  <li>Extract insights and actionable recommendations to drive profitability and customer retention</li>
</ol>

<h2>🛠️ Tools & Technologies</h2>

<ul>
  <li><b>Python</b> (<code>pandas</code>, <code>numpy</code>, <code>matplotlib</code>, <code>seaborn</code>) — Data cleaning, schema validation, and exploratory data analysis (EDA)</li>
  <li><b>Power BI</b> (Power Query / M, DAX) — Data modeling, KPI formulation, and dynamic report building</li>
</ul>

<h2>🗂️ Dataset</h2>

<ul>
  <li><b>Source:</b> FactSale dataset (transactional sales fact table)</li>
  <li><b>Size:</b> 26,397 rows × 21 columns</li>
  <li><b>Date range:</b> 2013-01-01 → 2016-05-31</li>
  <li><b>Grain:</b> One row per sale line item (product, customer, salesperson, dates, quantities, and financial metrics)</li>
</ul>

<h2>🧹 Data Cleaning</h2>

<!-- STYLED HTML/CSS TABLE -->
<div align="center">
  <table style="width: 100%; border-collapse: collapse; margin: 15px 0;">
    <thead>
      <tr style="background-color: #1f2937; color: #ffffff; text-align: left;">
        <th style="padding: 12px; border: 1px solid #374151;">Step</th>
        <th style="padding: 12px; border: 1px solid #374151;">Detail</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;"><b>Date columns</b></td>
        <td style="padding: 10px; border: 1px solid #374151;"><code>Invoice Date Key</code> and <code>Delivery Date Key</code> were stored as text → converted to proper <code>datetime</code> format</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;"><b>Missing values</b></td>
        <td style="padding: 10px; border: 1px solid #374151;">13 rows (0.05%) missing <code>Delivery Date Key</code> → imputed using the logical rule <code>Invoice Date + 1 day</code>, based on a 100% verified pattern in complete rows</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;"><b>Duplicates</b></td>
        <td style="padding: 10px; border: 1px solid #374151;">0 duplicate rows found; <code>drop_duplicates()</code> executed as a safeguard</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;"><b>Text formatting</b></td>
        <td style="padding: 10px; border: 1px solid #374151;">Trimmed extra whitespace and standardized string entries</td>
      </tr>
    </tbody>
  </table>
</div>

<h2>✅ Data Validation</h2>

<p>All calculated attributes were programmatically verified for internal consistency — <b>0 mismatches</b> found across all logical checks:</p>

<ul>
  <li><code>Tax Amount</code> = <code>Total Excluding Tax</code> × <code>Tax Rate</code></li>
  <li><code>Total Including Tax</code> = <code>Total Excluding Tax</code> + <code>Tax Amount</code></li>
  <li><code>Total Excluding Tax</code> = <code>Quantity</code> × <code>Unit Price</code></li>
  <li><code>Total Dry Items</code> + <code>Total Chiller Items</code> = <code>Quantity</code></li>
  <li><code>Delivery Date Key</code> &ge; <code>Invoice Date Key</code> (no logical temporal errors)</li>
  <li>No negative values in <code>Quantity</code>, <code>Unit Price</code>, or <code>Total</code> financial fields</li>
</ul>

<h3>Data Quality Issues Handled</h3>

<div align="center">
  <table style="width: 100%; border-collapse: collapse; margin: 15px 0;">
    <thead>
      <tr style="background-color: #1f2937; color: #ffffff; text-align: left;">
        <th style="padding: 12px; border: 1px solid #374151;">Issue</th>
        <th style="padding: 12px; border: 1px solid #374151;">Size</th>
        <th style="padding: 12px; border: 1px solid #374151;">Handling & Decision</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;">Date columns stored as text</td>
        <td style="padding: 10px; border: 1px solid #374151;">26,397 rows</td>
        <td style="padding: 10px; border: 1px solid #374151;">Parsed to datetime</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;">Missing <code>Delivery Date Key</code></td>
        <td style="padding: 10px; border: 1px solid #374151;">13 rows (0.05%)</td>
        <td style="padding: 10px; border: 1px solid #374151;">Imputed via <code>Invoice Date + 1 day</code> rule</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;">Duplicate rows</td>
        <td style="padding: 10px; border: 1px solid #374151;">0 rows</td>
        <td style="padding: 10px; border: 1px solid #374151;">Verified & protected via <code>drop_duplicates()</code></td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;">Negative <code>Profit</code> values</td>
        <td style="padding: 10px; border: 1px solid #374151;">566 rows (2.1%)</td>
        <td style="padding: 10px; border: 1px solid #374151;">Retained — represents actual loss-making transactions, not an anomaly</td>
      </tr>
      <tr>
        <td style="padding: 10px; border: 1px solid #374151;"><code>Customer Key</code> / <code>Bill To Customer Key</code> = 0</td>
        <td style="padding: 10px; border: 1px solid #374151;">9,077 rows (34.4%)</td>
        <td style="padding: 10px; border: 1px solid #374151;">Retained & segmented as <b>Walk-in</b> customers</td>
      </tr>
    </tbody>
  </table>
</div>

<h2>❓ Business Questions Solved</h2>

<p><b>Sales & Performance Over Time</b></p>
<ol>
  <li>What is the monthly/yearly trend for sales and profit? Is there a clear seasonality pattern?</li>
  <li>What are the top-performing months in terms of sales volume and total revenue?</li>
</ol>

<p><b>Product Analytics</b></p>
<ol start="3">
  <li>What are the top-selling products by volume versus profitability — are they identical?</li>
  <li>Which package type commands the highest market demand?</li>
</ol>

<p><b>Customer Segmentation</b></p>
<ol start="5">
  <li>What is the exact revenue split between registered customers and walk-in customers?</li>
</ol>

<p><b>Sales Team & Regional Performance</b></p>
<ol start="6">
  <li>Who are the top-performing sales representatives by revenue and profit margin contribution?</li>
  <li>Which cities generate the highest aggregate sales revenue?</li>
</ol>

<p><b>Profitability Analysis</b></p>
<ol start="8">
  <li>What is the net profit margin %, and which products or operational timeframes run at a loss?</li>
</ol>

<h2>📊 Dashboard Overview</h2>

<!-- STYLED IMAGE CONTAINER -->
<div align="center" style="margin: 20px 0;">
  <div style="background-color: #111827; padding: 10px; border-radius: 12px; border: 1px solid #374151; display: inline-block; max-width: 100%;">
    <img src="./dashboard_overview.jpeg" alt="Executive Overview & Sales Dashboard" style="width: 100%; height: auto; border-radius: 8px; display: block;" />
  </div>
  <p style="font-size: 0.85em; color: #9ca3af; margin-top: 8px;"><i>Figure 1: Executive Overview & Sales Dashboard View</i></p>
</div>

<p><b>Executive Overview includes:</b></p>
<ul>
  <li><b>Core KPI Cards:</b> Total Orders (26K), Total Sales ($20M), Total Profit ($10M), Profit Margin (50%), Total Quantity (1M)</li>
  <li><b>Financial Trends:</b> Multi-metric area/line chart tracking Profit, Revenue, and Margin % across 2013–2016</li>
  <li><b>Customer Segmentation:</b> Revenue share distribution (Walk-in: 66% vs Registered: 34%)</li>
  <li><b>Product Distribution:</b> Treemap breaking down total item quantities by package type (<code>Each</code>, <code>Pair</code>, <code>Bag</code>)</li>
  <li><b>Loss Monitoring:</b> Horizontal bar chart highlighting loss-making order frequency by month</li>
  <li><b>Slicers & Filters:</b> Interactive filtering by Package Type, Date Ranges, and Customer Types</li>
</ul>

<h2>💡 Key Insights</h2>

<ul>
  <li><b>Walk-in Dominance:</b> Unregistered/Walk-in customers drive <b>66% of total revenue ($13M)</b> despite lacking individual identity tracking.</li>
  <li><b>Healthy Margin Baseline:</b> Overall profit margin sits consistently around <b>50%</b>, showing strong pricing health across core categories.</li>
  <li><b>Seasonality in Losses:</b> Loss-making orders cluster heavily around specific months (e.g., May peaking at 73 orders), suggesting tactical pricing or promotional leakage during those periods.</li>
  <li><b>Package Concentration:</b> Demand is heavily concentrated in the <b>"Each"</b> packaging format, with minimal volume in secondary formats.</li>
</ul>

<h2>✅ Strategic Recommendations</h2>

<ul>
  <li><b>Walk-in Conversion Strategy:</b> Launch incentives (loyalty programs, instant discounts for registration) to convert Walk-in shoppers into registered profiles to unlock targeted marketing and LTV tracking.</li>
  <li><b>Loss Mitigation:</b> Audit pricing mechanics, discounts, and return rates in high-loss months (especially May and January) to fix margin leakage.</li>
  <li><b>Inventory Optimization:</b> Prioritize supply chain efficiency and warehouse stocking for top-demand package formats while reassessing underperforming packaging SKUs.</li>
  <li><b>Sales Coaching:</b> Document top sales reps' workflows to establish best-practice playbooks for training across underperforming territories.</li>
</ul>

<h2>📁 Repository Structure</h2>

<pre><code>├── FactSale.csv                     # Raw dataset
├── FactSale_Cleaned.csv             # Cleaned dataset
├── FactSales_Analysis.ipynb         # Python notebook: Cleaning, validation, EDA
├── FactSale_Cleaning_Report.docx    # Detailed validation & technical report
├── dashboard_overview.jpeg          # Power BI dashboard screenshot
└── README.md                        # Project documentation
</code></pre>
