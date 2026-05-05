# Sales Data Analysis – Power BI - DAX

## 📌 Project Overview

Perú CarHub, a car dealership based in Peru, requires two visual reports to monitor sales and customer activity. This project leverages two interactive dashboards: one highlighting the key drivers of sales performance and areas with lower impact, and another showcasing customer purchasing behavior. By utilizing Power BI’s data modeling, aggregation, and advanced DAX functions, the project delivers actionable insights to support strategic decision‑making.

## 🛠️ Tools & Technologies
- **Power BI Desktop**
  - **Power Query** –  Data preparation and transformation 
  - **Model View** – Management of relationships and data model structure.
  - **DAX (Data Analysis Expressions)** – Creation of advanced measures and calculated columns for analysis.
  - **Report View** – Design of interactive dashboards and KPI visualization.
- **GitHub** – Version control and public repository hosting.

## 📁Included Files

| File Name                 | Description                                                                |
|---------------------------|----------------------------------------------------------------------------|
| `ventas.xlsx`             | Clean dataset containing  Perú CarHub  data                                |
| `analisis_de_ventas.pbix` | It includes the data model and DAX analysis, as well as the sales and customer monitoring dashboards|
| `dashboard_and_tables.pdf`| Exported version of the dashboards|
| `modelo_de_datos.pdf `    | Star data model diagram                                                    |

## 🧭 Project Workflow

The **analisis_comercial.pbix** file contains the process of data preparation, exploration, transformation, analysis and visualization.

### 🔍 Data Preparation and Exploration
- Load the data model from the "ventas.xlsx" file and the following tables: "fact_ventas," "fact_presupuestos," "dim_canal," "dim_cliente," "dim_sede," "dim_vehiculo," "dim_vendedor," and "foto_vehiculos".
-	Review each table in the model to understand the information contained in each one.
-	Check the data types and assign the correct ones.
-	Combine the period and month columns from the fact_presupuesto table and generate the column fecha_presupuesto, with date format.
-	Change the format of the "nombre_sede" column in the "dim_sede" table to "Capitalize Each Word".
-	Explore the star schema data model and define the relationships and cardinality between fact and dimension tables.

  
### 🔄 Data Transformation
-	Create the calculated table dim_fechas, which contains a calendar with dates from 01/01/2015 to 12/31/2017, using date data type and short date format.
-	Create Calculated Columns – *dim_fechas*

| Column Name     | Function / Expression                           | Description                        |
|-----------------|-------------------------------------------------|------------------------------------|
| `Año`           | Año = YEAR(dim_fechas[Date])                  | Extracts the year from the date    |
| `Trimestre`     | Trimestre = "T" & QUARTER(dim_fechas[Date])   | Returns the quarter number (1–4)   |
| `NumeroMes`     | MONTH(dim_fechas[Date])`                      | Returns the month number (1–12)    |
| `Mes`           | FORMAT(dim_fechas[Date],"mmmm")               | Displays the full month name       |
| `NumeroSemana`  | WEEKNUM(dim_fechas[Date],2)                   | Returns the week number of the year|
| `Día`           | FORMAT(Dim_Fechas[Date],"dddd")               | Displays the full day name         |
| `DateKey`       | VALUE(FORMAT(dim_fechas[Date],"yyyymmdd"))    | Creates a numeric key for the date |

-	Manage the relationships of the star schema data model by establishing the relationships and cardinality between the "dim_fechas" and "fact_ventas" and "fact_presupuesto" tables.

### 📈 Analysis
Repository of calculated measures created using DAX:
  
| Measure Name                | Function(s)                                                       | Description                                                 |
|-----------------------------|-------------------------------------------------------------------|-------------------------------------------------------------|
| `Total de Ventas`           | SUM(fact_ventas[Precio Venta sin IGV])                         | Calculates the total sales amount                           |
| `Cantidad Clientes`         | DISTINCTCOUNT(fact_ventas[Cliente])                            | Counts the number of unique clients                         |
| `Cumplimiento`              | DIVIDE([Total de Ventas],[Total Presupuesto])     | Measures the percentage of sales achievement against the budget           |
| `YoY`      |VAR VentasLY = CALCULATE([Total de Ventas], DATEADD(Dim_Fechas[Date],-1,YEAR)) RETURN DIVIDE([Total de Ventas]-VentasLY, VentasLY,0) |Year-over-year variation in sales|
| `Venta del Mes Anterior`| CALCULATE([Total de Ventas],PARALLELPERIOD(Dim_Fechas[Date],-1,MONTH))| Sales of the same month in the previous year|
| `Crecimiento Mensual` |[Total de Ventas]- [Venta del Mes Anterior]| monthly growth compared to the same month of the previous year|


### 📊 Data Visualization

| Chart Type            | Title                                                               | Description                                                     |
|-----------------------|---------------------------------------------------------------------|-----------------------------------------------------------------|
| Card                  | Total de Ventas<br>Clientes<br>Cumplimiento<br>Variación Interanual |Displays the total sales amount<br>Displays the number of clients<br>Displays the percentage of sales achievement against the budget<br>Displays the year-over-year variation in sales|
| Clustered column chart| Comparativa de Ventas por Mes|Displays current month sales, sales of the same month in the previous year, and monthly growth|
| Stacked bar chart  |Top 5 Ventas por Modelo de vehículo                        | Displays the five vehicle models that generated the most sales|
| Stacked column chart  |Ventas por Marca de Vehículo                       | Displays how sales are distributed by vehicle brand in each quarter|
| Pie Chart             | Ventas por Segmento                                               | Displays the proportion of sales by type of cliente|
| Map Chart    | Ventas por Sede                                                     | Displays sales by location                                |


## 🧠 Key Insights 

  - 87% of clients are individuals, while 13% are companies.
  - The top-performing branch is Santiago de Surco, which leads in total sales volume. The branch with the lowest performance is La Molina.
  - Toyota and Suzuki are the best-selling brands, indicating strong customer preference. Mazda is the least-selling brand.


## 🚀 Execution Guide 

To explore this project in full:
- Open the analisis_de_ventas.pbix Power BI file.
- Navigate through each view:
    - Report view: Displays the dashboard on one page and two tables on the other page. The tables display some of the calculated measures.
    - Table view: Displays the tables that make up the star schema data model.
    - Model view: Star schema data model.

The contents of each file are explained in detail in the **Included Files** section.
    
