# Sales Data Analysis – Power BI 

## 📌 Project Overview

Peru CarHub, a car dealership based in Peru, required a visual report to gain insight into its sales activity. For this project, I developed an interactive dashboard highlighting the main drivers of sales performance and the areas with the least impact. The project uses data modelling and advanced DAX functions to provide actionable insights and support strategic decision-making.

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
| `analisis_de_ventas.pbix` | It includes the data model and DAX analysis, as well as the sales dashboards|
| `dashboard_and_tables.pdf`| Exported version of the dashboard|
| `modelo_de_datos.pdf `    | Star data model diagram                                                    |

## 🧭 Project Workflow

The **analisis_de_ventas.pbix** file contains the process of data preparation, exploration, transformation, analysis and visualization.

### 🔍 Data Exploration and Preparation  
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

- **Filters**This dashboard includes filters by year and month, vehicle brand, and location.

| Chart Type            | Title                                                               | Description                                              |
|-----------------------|---------------------------------------------------------------------|----------------------------------------------------------|
| Card                  | Total de Ventas<br>Cumplimiento<br>YoY |Displays the total sales amount<br>Displays the percentage of sales achievement against the budget<br>Displays the year-over-year variation in sales|
| Clustered column chart| Comparativa de Ventas por Mes|Displays current month sales, sales of the same month in the previous year, and monthly growth|
| Stacked bar chart  |Top 5 Ventas por Modelo de vehículo                        | Displays the five vehicle models that generated the most sales|
| Stacked column chart  |Ventas por Marca de Vehículo                       | Displays how sales are distributed by vehicle brand in each quarter|
| Pie Chart             | Ventas por Segmento                                               | Displays the proportion of sales by customer type|
| Map Chart             | Ventas por Sede                                                     | Displays sales by location             |                             

## 🧠 Key Insights 
 
  - The Top-performing vehicle models by sales are: Genesis (Hyundai), XL7 (Suzuki), Elantra (Hyundai), Santa Fe (Hyundai) and 251–650 (Suzuki). The top 5 models together account for 17 % of total sales, highlighting the importance of a few key products.
  - Toyota and Suzuki are the best-selling brands, indicating strong customer preference, while Mazda is the least-selling brand.
  - Toyota leads the way in overall sales thanks to its diverse range of models, even though none of them feature in the top five best-sellers.
  - 87.01 % of sales come from individual customers, while only 12.99% come from corporate customers.
  - Santiago de Surco is the best-performing branch, leading in total sales volume with 58.36%. Sales at the other three branches — Ate (16.75%), San Miguel (16.65%) and La Molina (8.24%) — don't exceed Santiago de Surco's.

- **Strategic Interpretation:**

- Design promotional strategies that are specific to the vehicle models with the highest sales performance.
- Highlight Toyota's diversity strategy and analyze which models support it to optimize inventory.
- Focus marketing campaigns and promotions on individual customers, as they represent the majority of the market.
- Evaluate strategies to improve sales performance at the La Molina branch.


## 🚀 Execution Guide 

To explore this project in full:
- Open the analisis_de_ventas.pbix Power BI file.
- Navigate through each view:
    - Report view: Displays the dashboard.
    - Table view: Displays the tables that make up the star schema data model.
    - Model view: Star schema data model.

The contents of each file are explained in detail in the **Included Files** section.
    
