# TAT Dashboard

Streamlit web app for analyzing **Dispatch & Delivery Turnaround Time (TAT)** from a sales report.

## Features

- **Two parent toggles**: Dispatch TAT and Delivery TAT (separate bucket logic for each)
- **4 sub-views per TAT**: Invoice Date, MIS Item Group, Sales Channel, From Warehouse
- **Customer drill-down** inside the Sales Channel tab
- **Smart sidebar filters** with search, Select All / None, all-selected-by-default, cascading Customer from Sales Channel
- **Date presets**: All Time, Last 7 / 15 / 30 Days, Custom range
- **Dark bold table headers** in both the dashboard and Excel export
- **Pivot-only Excel download** with formatted sheets for both TAT types

## Bucket Logic

| TAT type     | Buckets                                                  | Source column   |
| ------------ | -------------------------------------------------------- | --------------- |
| Dispatch TAT | `0-2 Days`, `3-5 Days`, `>5 Days`                         | `Dis Days`      |
| Delivery TAT | `0-9 Days`, `10-12 Days`, `>12 Days`, `Delivery Pending` | `Delivery Days` |

## Required columns in upload

`Invoice Date`, `New MIS Item Group`, `Sales_Channel`, `From Warehouse`, `Customer`,
plus `Dis Days` / `Dis TAT` and `Delivery Days` / `Delivery TAT`.

## Install & run

```bash
pip install -r requirements.txt
streamlit run app.py
```

The app opens at http://localhost:8501.
