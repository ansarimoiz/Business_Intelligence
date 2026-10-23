# Brazilian E-Commerce Analytics Dashboard | Power BI

An interactive Power BI dashboard built using the Brazilian E-Commerce Public Dataset by Olist. This project analyzes marketplace sales, product and customer performance, delivery operations, and customer satisfaction through an interactive, multi-page business intelligence report.

## Dashboard Preview

### 1. Executive Overview
<!-- <h3>Executive Overview</h3> -->

<img width="1352" alt="Executive Overview" src="https://github.com/user-attachments/assets/749fa22c-5d36-43fc-9ec9-1aac296f300f" />

Provides a consolidated view of marketplace performance, including sales, order volume, delivery metrics, average review scores, monthly sales trends, and product category performance.

### 2. Product & Customer Analytics

![Product & Customer Analytics](https://github.com/user-attachments/assets/8cf8c033-be2a-4fd1-b0cd-8c698b39c633)

Explores product category performance, sales distribution, customer purchasing patterns, average review scores, and product-level metrics. Interactive filters allow users to investigate performance across categories and products.

### 3. Delivery & Customer Experience

![Delivery & Customer Experience](https://github.com/user-attachments/assets/de3c778b-2f8a-447d-ae1a-4c25a93668c7)

Evaluates delivery performance through on-time delivery rates, late deliveries, average delivery duration, geographic delivery performance, and customer review scores across delivery-delay categories.

## Data Model & Semantic Model

The report uses a relational semantic model designed to support analysis across orders, order items, products, customers, sellers, payments, reviews, and delivery performance.

![Power BI Semantic Model](<img width="740" height="734" alt="image" src="https://github.com/user-attachments/assets/9d7a3a15-6b2c-4c69-a8fd-425505e4ebff" />
)

### Star Schema & Relationships

The model follows a dimensional modeling approach, separating descriptive dimensions from transactional data while maintaining distinct fact-table grains.

**Dimension tables**
- `dimDate` — calendar attributes for time-based reporting.
- `Customers` — customer identifiers and geographic attributes.
- `Products` — product attributes and translated product categories.
- `Sellers` — seller identifiers and geographic attributes.

**Transactional tables**
- `Orders` — order status, purchase timestamps, and delivery timestamps.
- `Order Items` — item-level transactions, product and seller references, prices, and freight values.
- `Payments` — payment methods, payment values, and installment information.
- `Order Reviews` — customer review scores and review timestamps.

Relationships use business keys such as `order_id`, `customer_id`, `product_id`, and `seller_id`, with appropriate cardinalities and filter directions to support interactive reporting.

The model preserves the grain of each transactional table to reduce double-counting when analyzing different aspects of marketplace performance. For example, order-level delivery metrics are calculated from `Orders`, while product revenue is calculated from `Order Items` and payment metrics are calculated from `Payments`.

### Dedicated DAX Measure Table
<img width="298" height="443" alt="image" src="https://github.com/user-attachments/assets/aa0dd8eb-d5a6-4d8d-8288-f1b9b9b75534" />

A separate, dedicated measure table is used to organize DAX measures independently of the source data tables.

This keeps calculations centralized and easier to maintain, improves discoverability in the Fields pane, and separates business logic from the underlying data structure.

Measures cover key analytical metrics such as:
- Sales and revenue aggregation
- Distinct order and customer counts
- Average order value and items per order
- Delivery rates and delivery duration
- Late delivery analysis
- Average customer review scores
- Repeat customer analysis

## Dynamic Time Aggregation with Field Parameters

A field parameter enables users to dynamically change the time granularity of supported charts without creating separate visuals for each time period.

The parameter switches the chart axis between fields from the `dimDate` table:

- **Year** — annual performance comparisons
- **Quarter** — quarterly trends
- **Month** — monthly performance analysis

Users can switch between Year, Quarter, and Month using a selector, allowing the same visual to display data at different levels of aggregation.

This provides a more flexible reporting experience, reduces visual duplication, and enables users to move between high-level performance trends and more detailed time-based analysis.

## Key Business Questions

The dashboard is designed to help answer questions such as:

- How are sales and order volumes changing over time?
- Which product categories contribute most to marketplace sales?
- How does customer purchasing behavior vary across products and categories?
- What proportion of delivered orders arrive on time?
- Which customer states experience higher late delivery rates?
- How are customer review scores associated with delivery delays?
- Which operational areas may require further investigation?

## Tools & Technical Skills

- **Power BI Desktop** — report development and interactive visualizations
- **DAX** — measures, calculated columns, and KPI calculations
- **Power Query** — data preparation and transformation
- **Dimensional Modeling** — fact and dimension tables, relationship design, and granularity management
- **Semantic Modeling** — reusable measures and controlled filter propagation
- **Field Parameters** — dynamic Year, Quarter, and Month aggregation
- **Data Visualization** — KPI cards, trend charts, category comparisons, and geographic analysis
- **Business Intelligence** — sales reporting, delivery performance, and customer experience analysis

## Data Source

**Brazilian E-Commerce Public Dataset by Olist**

Source: [Kaggle — Brazilian E-Commerce Public Dataset by Olist](https://www.kaggle.com/datasets/olistbr/brazilian-ecommerce)

The dataset contains historical Brazilian marketplace data from 2016–2018, including orders, order items, products, customers, sellers, payments, reviews, and delivery timestamps.

The dataset is used for analytical and portfolio purposes. Please refer to the original source for its terms and attribution requirements.

## Repository Structure

```text
olist-ecommerce-powerbi-dashboard/
├── README.md
├── dashboard/
│   └── Olist_Ecommerce_Dashboard.pbix
├── screenshots/
│   ├── executive-overview.png
│   ├── product-customer-analytics.png
│   ├── delivery-customer-experience.png
│   ├── semantic-model.png
│   └── measure-table.png
├── dax/
│   └── measures.dax
└── docs/
    └── data-model.md
```

## Business Metric Definitions & Limitations

- Sales are calculated from the available item price and freight fields. They should not be interpreted as net profit because product cost data is not provided.
- Delivery performance is evaluated using actual delivery timestamps against estimated delivery dates.
- Average review scores represent order-level customer feedback and are not necessarily product-specific ratings.
- Delivery-delay analysis identifies associations between delivery timing and review scores; it does not establish causation.
- The dataset represents historical marketplace activity and does not provide live operational data.

## Project Objective

This project demonstrates the application of Power BI to a multi-table business dataset, with an emphasis on dimensional modeling, reusable DAX calculations, dynamic time aggregation, interactive reporting, and actionable business insights.

The goal is to build a maintainable and business-oriented BI solution rather than a collection of standalone charts.
 
