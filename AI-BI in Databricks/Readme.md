# Databricks System‑Tables Insights Dashboard

This repository contains a Databricks AI/BI Dashboard (a `.lvdash.json` file) that visualises key metrics from Databricks system tables.  The dashboard surfaces cost, usage, reliability and performance information directly from Unity Catalog‑managed tables, making it easy to monitor your Databricks estate without exporting data to a separate BI tool.

## Why Databricks Dashboards?

- **Native and near‑real‑time** – Dashboards run directly against your system tables in the lakehouse.  There’s no need for daily extracts or an external BI server, and you always see the most up‑to‑date information.
- **Unified governance** – Permissions on the underlying tables carry through to the visuals, so you don’t have to duplicate row‑level security rules in another system.
- **Interactive and self‑service** – Built‑in filters, cross‑filtering and responsive charts let business users slice and drill into the data themselves.
- **Cost‑effective** – Dashboards are part of Databricks SQL, so there are no additional licensing fees or servers to manage. They’re an ideal starting point before migrating from legacy BI platforms.

## Dashboard Structure

The dashboard is organised into three pages:

### 1. Read Me

A landing page that summarises the purpose of the dashboard and how to use it.  It highlights:

- **Overview** – Explains that metrics are pulled from system tables to monitor cost, usage, reliability and performance.
- **Business Overview** – Describes the high‑level metrics available to executives.
- **Technical & Performance** – Describes the detailed compute and query metrics for engineers and SREs.
- **How to Use** – Provides tips for filtering, cross‑filtering, and interpreting spikes or anomalies.

### 2. Business Overview

A high‑level view of costs, usage and reliability.  Key components:

- **KPI Tiles** – Cost USD, DBUs consumed, USD per DBU, Pipeline Success Rate, Job Success Rate, Job P95 Sec, Query P95 (ms).  These tiles give an at‑a‑glance view of efficiency and reliability.
- **Filters** – A date range picker and a multi‑select filter for SKU (e.g. Jobs, Pipelines, SQL Warehouses).  These filters affect all downstream charts.
- **Job Health Summary** – A table showing each job’s total runs, failed runs, failure rate and 95th‑percentile duration over the past 30 days.  Sort by failure rate or P95 to find problematic jobs quickly.
- **Daily Cost & DBUs by SKU** – Bar and line charts show spend and consumption trends.  If cost rises while DBUs remain flat, unit prices may have increased or workloads may be inefficient.
- **Job and Pipeline Reliability** – Dual line charts show daily success rates and P95 runtimes for jobs and pipelines.
- **Task Mix** – A bar chart summarising the count of different task keys (notebooks, Python wheels, DLT pipelines, etc.).
- **Cost Attribution** – A pie chart breaking down DBU spend by object type (Jobs, Pipelines, Warehouses, Other).
- **Top Users by Cost** – A bar chart ranking the top spenders (users or service principals) using the `identity_metadata.run_as` field.
- **Top Jobs by Cost (last 30 days)** – A bar chart showing the top jobs by DBU cost.  This helps identify cost drivers at the job level.

### 3. Technical & Performance

This page dives into compute and query behaviour:

- **Warehouse Running Ratio** – Line chart showing the percentage of time each warehouse spends in a `RUNNING` state each day.  High ratios with few queries suggest over‑provisioning.
- **Node CPU vs Memory Utilisation** – Scatter plot of average CPU versus memory utilisation per cluster over the last seven days.  Easily spot over‑ and under‑sized clusters.
- **Average CPU Usage by Hour** – Highlights daily peaks and troughs to optimise job scheduling or auto‑scaling settings.
- **Query Duration vs Rows Read** – Scatter plot comparing query duration with rows scanned.  Filter by query status (finished, failed, cancelled) to isolate problematic queries.
- **Query P95 Duration & Failure Counts** – A combo chart with a line for 95th‑percentile query duration and bars for daily failed queries.  Spikes indicate regressions or bottlenecks.
- **Warehouse Efficiency & Idle Ratio** – Charts comparing run time against query volumes.  A high idle ratio means the warehouse is running but underutilised, signalling you should adjust auto‑stop settings.
- **Successful and Failed Jobs Tables** – Two tables list jobs with the most successful runs and most failed runs, along with total run counts.
- **Cluster Utilisation Breakdown** – Bar chart showing the percentage of clusters that are over‑utilised (>80 % CPU), under‑utilised (<20 % CPU) or optimal.  Helps identify opportunities to resize or consolidate clusters.

## How to Use

1. **Import the dashboard**: In Databricks SQL, go to **Dashboards → Import** and choose the `.lvdash.json` file provided in this repository to import it into your workspace.
2. **Apply filters**: Use the date range picker and SKU selector on the Business Overview page to restrict the analysis.  All charts will update accordingly.
3. **Cross‑filter**: Click on a bar or point in a chart to filter other charts to the same time slice or category.  For example, clicking a spike in the Query Duration vs Rows Read plot filters all charts to that date, helping you trace performance issues to specific jobs or pipelines.
4. **Investigate anomalies**: Sort the Job Health Summary by failure rate or P95 duration to identify unstable jobs.  Look at the Top Jobs by Cost or Top Users by Cost to control spend.  Examine the Cluster Utilisation Breakdown to detect over‑ or under‑provisioned compute.

## Updating or Extending the Dashboard

The dashboard is defined in a single `.lvdash.json` file.  To modify it:

- **Edit datasets**: Each dataset has a `queryLines` array.  You can adjust the SQL to add new metrics or fix logic errors.  For example, changing the time window or grouping logic.
- **Adjust layouts**: In the `pages.layout` section, each widget has `x`, `y`, `width` and `height` coordinates on a 12‑column grid.  Modify these to rearrange the dashboard.
- **Add visuals**: Create new datasets for additional insights (e.g. Top Pipelines by Cost) and reference them in new widgets.  Supported widget types include counters, line charts, bars, pies, tables and scatter plots.

Feel free to clone this repository and adapt the dashboard to your own use cases.  It’s a powerful way to pilot native Databricks reporting before deprecating legacy BI tools.

