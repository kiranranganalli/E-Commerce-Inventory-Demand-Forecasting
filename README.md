                +-----------------------+
                |   S3 Data Lake        |
                | (raw_inventory.json)  |
                +----------+------------+
                           |
                           ▼
               +----------------------+
               |   AWS Glue Job       |
               | PySpark ETL Pipeline |
               +----------------------+
                           |
                           ▼
          +-----------------------------+
          |     Redshift Warehouse      |
          |   (sku_demand_forecast)     |
          +-----------------------------+
                           |
                           ▼
         +-------------------------------+
         |     Tableau Dashboard         |
         | Demand Shock & Inventory Plan |
         +-------------------------------+



---

## 📂 Project Structure

.
├── README.md                      # Project overview and documentation
├── forecast_pipeline.py           # PySpark-based ETL and demand forecasting logic
├── forecast_metrics.csv           # Output: Forecasted demand (SKU x Region x Date)
├── sku_metadata.csv               # Input: SKU metadata (category, lead time, supplier)
└── dashboard_forecasting.twbx     # Tableau scenario planner for procurement simulation


---

## 🔍 Key Features

| Feature                              | Description                                                                 |
|--------------------------------------|-----------------------------------------------------------------------------|
| 📊 **Forecast Modeling**            | Aggregates 200,000+ daily records to simulate future demand by region.     |
| 🔁 **Inventory Flow Simulation**     | Models lead times, reorder points, and safety stock per SKU.               |
| 🔮 **Shock Scenario Planning**       | Simulate sudden demand surges (e.g., viral events, holiday spikes).        |
| ⚠️ **Out-of-Stock Risk Detection**   | Tags high-risk SKUs and calculates replenishment buffers.                   |
| 📈 **Tableau Planning Interface**    | Visualizes demand shocks and operational tradeoffs in real time.           |

---

## 📥 Sample Data

- `forecast_metrics.csv` — Forecasted daily demand by SKU, Region, Date
- `sku_metadata.csv` — SKU → Category, Procurement Lead Time, Supplier Info

Sample snippet:

| sku_id | region | date       | forecast_demand | stock_on_hand | risk_level |
|--------|--------|------------|------------------|----------------|------------|
| SKU123 | West   | 2025-08-01 | 112              | 89             | Medium     |
| SKU456 | East   | 2025-08-01 | 342              | 210            | High       |

---

## ⚙️ Technologies Used

- **AWS Glue** – Distributed data processing using PySpark
- **Amazon S3** – Input/output storage for simulation data
- **Amazon Redshift** – Forecast result warehouse
- **PySpark** – ETL logic, demand forecasting
- **Tableau** – Simulation dashboard for demand planning

---

## 📌 How It Works

1. **Ingestion:** Historical and synthetic SKU data ingested from S3.
2. **Transformation:** Aggregates by day, category, region using PySpark.
3. **Forecasting Logic:** 
   - Applies exponential smoothing
   - Accounts for lead time buffers and promotions
4. **Risk Tagging:** Labels SKUs as High/Medium/Low risk based on stock position and demand volatility.
5. **Dashboard Feed:** Outputs pushed to Redshift and visualized in Tableau.

---

## 📊 Tableau Dashboard Preview

Key Visuals:
- Forecast vs Actual by SKU and Region
- Stockout Heatmap (SKU x Date)
- Procurement Optimization Planner
- Demand Shock Toggle (what-if simulation)

---

## 🧪 Example Use Case

> “A sudden TikTok campaign causes a 70% spike in demand for a specific category in the West region. The pipeline flags affected SKUs, adjusts reorder quantities, and updates Tableau for stakeholder review—all within one scheduled run.”

---

## ✅ Outcomes

- Improved stockout risk visibility for 10,000+ SKUs
- Reduced overstock waste through forecast-optimized procurement
- Enabled faster scenario response (e.g., flash sales, promotions)
- Enhanced collaboration between planners and procurement

---

## 📎 License

This project is licensed under the MIT License.

---

## 🙋‍♂️ Contact

**Kiran Ranganalli**  
Email: [Your Email]  
GitHub: [github.com/yourusername](https://github.com/yourusername)

---

