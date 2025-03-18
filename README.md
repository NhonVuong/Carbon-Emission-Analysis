# Carbon-Emission-Analysis
![image](https://github.com/NhonVuong/Carbon-Emission-Analysis/blob/main/cover.jpg)
This report aims to analyze carbon emissions to examine the carbon footprint across various industries. We aim to identify sectors with the highest levels of emissions by analyzing them across countries and years, as well as to uncover trends.

Carbon emissions play a crucial role in the environment, accounting for over 75% of global emissions and posing a significant environmental challenge. These emissions contribute to the accumulation of greenhouse gases in the atmosphere, leading to climate change, planetary warming, and involvement in various environmental disasters.

Through this analysis, we hope to gain an understanding of the environmental impact of different industries and contribute to making informed decisions in sustainable development.


***

## **Data Structure**

The dataset consists of 4 tables containing information regarding carbon emissions generated during the production of goods.

![image](https://github.com/NhonVuong/Carbon-Emission-Analysis/blob/main/Database%20diagram.png)

#### Table 'product_emissions'

```
SELECT * FROM product_emissions LIMIT 3
```

| id           | company_id | country_id | industry_group_id | year | product_name                                                    | weight_kg | carbon_footprint_pcf | upstream_percent_total_pcf | operations_percent_total_pcf | downstream_percent_total_pcf | 
| -----------: | ---------: | ---------: | ----------------: | ---: | --------------------------------------------------------------: | --------: | -------------------: | -------------------------: | ---------------------------: | ---------------------------: | 
| 10056-1-2014 | 82         | 28         | 2                 | 2014 | Frosted Flakes(R) Cereal                                        | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10056-1-2015 | 82         | 28         | 15                | 2015 | "Frosted Flakes, 23 oz, produced in Lancaster, PA (one carton)" | 0.7485    | 2                    | 57.50                      | 30.00                        | 12.50                        | 
| 10222-1-2013 | 83         | 28         | 8                 | 2013 | Office Chair                                                    | 20.68     | 73                   | 80.63                      | 17.36                        | 2.01                         | 

#### Table 'industry_groups'

```
SELECT * FROM industry_groups LIMIT 3
```

| id | industry_group                                                         | 
| -: | ---------------------------------------------------------------------: | 
| 1  | "Consumer Durables, Household and Personal Products"                   | 
| 2  | "Food, Beverage & Tobacco"                                             | 
| 3  | "Forest and Paper Products - Forestry, Timber, Pulp and Paper, Rubber" | 

#### Table 'companies'

```
SELECT * FROM companies LIMIT 3
```
| id | company_name               | 
| -: | -------------------------: | 
| 1  | "Autodesk, Inc."           | 
| 2  | "Casio Computer Co., Ltd." | 
| 3  | "Cisco Systems, Inc."      | 

#### Table 'countries'

```
SELECT * FROM countries LIMIT 3
```

| id | country_name | 
| -: | -----------: | 
| 1  | Australia    | 
| 2  | Belgium      | 
| 3  | Brazil       | 

##### 1. Which products contribute the most to carbon emissions?

```
SELECT product_name, 
       ROUND(AVG(carbon_footprint_pcf),2) AS avg_carbon_footprint_pcf
FROM product_emissions
GROUP BY product_name
ORDER BY avg_carbon_footprint_pcf DESC
LIMIT 10;
```

| product_name                                                                                                                       | avg_carbon_footprint_pcf | 
| ---------------------------------------------------------------------------------------------------------------------------------: | -------------------------: | 
| Wind Turbine G128 5 Megawats                                                                                                       | 3718044.00                 | 
| Wind Turbine G132 5 Megawats                                                                                                       | 3276187.00                 | 
| Wind Turbine G114 2 Megawats                                                                                                       | 1532608.00                 | 
| Wind Turbine G90 2 Megawats                                                                                                        | 1251625.00                 | 
| Land Cruiser Prado. FJ Cruiser. Dyna trucks. Toyoace.IMV def unit.                                                                 | 191687.00                  | 
| Retaining wall structure with a main wall (sheet pile): 136 tonnes of steel sheet piles and 4 tonnes of tierods per 100 meter wall | 167000.00                  | 
| TCDE                                                                                                                               | 99075.00                   | 
| Mercedes-Benz GLE (GLE 500 4MATIC)                                                                                                 | 91000.00                   | 
| Mercedes-Benz S-Class (S 500)                                                                                                      | 85000.00                   | 
| Mercedes-Benz SL (SL 350)                                                                                                          | 72000.00                   | 

##### 2. What are the industry groups of these products?

```
SELECT ig.industry_group, 
    	ROUND(AVG(pe.carbon_footprint_pcf),2) AS avg_carbon_footprint_pcf
FROM product_emissions pe
JOIN industry_groups ig ON pe.industry_group_id = ig.id
GROUP BY ig.industry_group
ORDER BY avg_carbon_footprint_pcf DESC
LIMIT 10;
```

| industry_group                                   | avg_carbon_footprint_pcf | 
| -----------------------------------------------: | -----------------------: | 
| Electrical Equipment and Machinery               | 891050.73                | 
| Automobiles & Components                         | 35373.48                 | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 24162.00                 | 
| Capital Goods                                    | 7391.77                  | 
| Materials                                        | 3208.86                  | 
| "Mining - Iron, Aluminum, Other Metals"          | 2727.00                  | 
| Energy                                           | 2154.80                  | 
| Chemicals                                        | 1949.03                  | 
| Media                                            | 1534.47                  | 
| Software & Services                              | 1368.94                  | 

##### 3. What are the industries with the highest contribution to carbon emissions?

```
SELECT ig.industry_group, 
    	ROUND(AVG(pe.carbon_footprint_pcf),2) AS avg_carbon_footprint_pcf
FROM product_emissions pe
JOIN industry_groups ig ON pe.industry_group_id = ig.id
GROUP BY ig.industry_group
ORDER BY avg_carbon_footprint_pcf DESC
LIMIT 10;
```

| industry_group                                   | avg_carbon_footprint_pcf | 
| -----------------------------------------------: | -----------------------: | 
| Electrical Equipment and Machinery               | 891050.73                | 
| Automobiles & Components                         | 35373.48                 | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | 24162.00                 | 
| Capital Goods                                    | 7391.77                  | 
| Materials                                        | 3208.86                  | 
| "Mining - Iron, Aluminum, Other Metals"          | 2727.00                  | 
| Energy                                           | 2154.80                  | 
| Chemicals                                        | 1949.03                  | 
| Media                                            | 1534.47                  | 
| Software & Services                              | 1368.94                  | 

##### 4. What are the companies with the highest contribution to carbon emissions?

```
SELECT c.company_name, 
    	ROUND(AVG(pe.carbon_footprint_pcf),2) AS avg_carbon_footprint_pcf
FROM product_emissions pe
JOIN companies c ON pe.company_id = c.id
GROUP BY c.company_name
ORDER BY avg_carbon_footprint_pcf DESC
LIMIT 10;
```

| company_name                           | avg_carbon_footprint_pcf | 
| -------------------------------------: | -----------------------: | 
| "Gamesa Corporación Tecnológica, S.A." | 2444616.00               | 
| "Hino Motors, Ltd."                    | 191687.00                | 
| Arcelor Mittal                         | 83503.50                 | 
| Weg S/A                                | 53551.67                 | 
| Daimler AG                             | 43089.19                 | 
| General Motors Company                 | 34251.75                 | 
| Volkswagen AG                          | 26238.40                 | 
| Waters Corporation                     | 24162.00                 | 
| "Daikin Industries, Ltd."              | 17600.00                 | 
| CJ Cheiljedang                         | 15802.83                 | 

##### 5. What are the countries with the highest contribution to carbon emissions?

```
SELECT co.country_name, 
    	ROUND(AVG(pe.carbon_footprint_pcf),2) AS avg_carbon_footprint_pcf
FROM product_emissions pe
JOIN countries co ON pe.country_id = co.id
GROUP BY co.country_name
ORDER BY avg_carbon_footprint_pcf DESC
LIMIT 10;
```

| country_name | avg_carbon_footprint_pcf | 
| -----------: | -----------------------: | 
| Spain        | 699009.29                | 
| Luxembourg   | 83503.50                 | 
| Germany      | 33600.37                 | 
| Brazil       | 9407.61                  | 
| South Korea  | 5665.61                  | 
| Japan        | 4600.26                  | 
| Netherlands  | 2011.91                  | 
| India        | 1535.88                  | 
| USA          | 1332.60                  | 
| South Africa | 1119.27                  | 

##### 6. What is the trend of carbon footprints (PCFs) over the years?

```
SELECT year, COUNT(product_name) product_name, SUM(avg_carbon_footprint_pcf) sum_pcf
FROM (
	  SELECT year, product_name, 
			  ROUND(AVG(carbon_footprint_pcf),2) AS avg_carbon_footprint_pcf
	  FROM product_emissions 
	  GROUP BY year, product_name
  	 ) AS tb
GROUP BY year
```

| year | product_name | sum_pcf     | 
| ---: | -----------: | ----------: | 
| 2013 | 176          | 496005.50   | 
| 2014 | 186          | 548213.50   | 
| 2015 | 217          | 10810407.00 | 
| 2016 | 215          | 1608962.17  | 
| 2017 | 57           | 224799.67   | 

##### 7. Which industry groups has demonstrated the most notable decrease in carbon footprints (PCFs) over time?

```
WITH raw_data AS (
SELECT year,
	  ig.industry_group,
	  AVG(pe.carbon_footprint_pcf) AS avg_pcf
FROM product_emissions pe
JOIN industry_groups ig ON ig. id = pe. industry_group_id
GROUP BY year, industry_group
	)
SELECT cy.industry_group,
--		cy.year AS current_year,
--		cy.avg_pcf AS current_year_avg_pef,
--		lst_y.avg_pcf AS last_year_avg_pcf,
		SUM(lst_y.avg_pcf - cy.avg_pcf) AS delta_pcf
FROM raw_data cy
LEFT JOIN raw_data lst_y ON cy.year - 1 = lst_y.year AND cy.industry_group = lst_y.industry_group
GROUP BY industry_group
HAVING delta_pcf IS NOT NULL
ORDER BY delta_pcf
```

| industry_group                                   | delta_pcf   | 
| -----------------------------------------------: | ----------: | 
| "Pharmaceuticals, Biotechnology & Life Sciences" | -24079.5000 | 
| Automobiles & Components                         | -14100.2857 | 
| Capital Goods                                    | -13973.9667 | 
| Materials                                        | -7152.8791  | 
| Software & Services                              | -688.5000   | 
| Commercial & Professional Services               | -248.7917   | 
| "Food, Beverage & Tobacco"                       | -49.4820    | 
| Retailing                                        | 0.8333      | 
| Telecommunication Services                       | 6.2500      | 
| Food & Staples Retailing                         | 76.8000     | 
| Consumer Durables & Apparel                      | 173.5966    | 
| Technology Hardware & Equipment                  | 265.1054    | 
| Media                                            | 1808.5833   | 

##### The products with the highest levels of carbon emissions are typically associated with heavy industry.

* Products with the highest CO2 emissions typically come from steel, chemicals, lithium batteries, and industrial materials.
* Metal & chemical products have the highest emissions due to energy-intensive production processes.
* Batteries and electronic components have a large carbon footprint due to lithium, cobalt mining, and complex manufacturing.


##### The Following Car Models Are Leading in Carbon Emissions During Production

* The following car models are leading in carbon emissions during production: Land Cruiser Prado, Mercedes-Benz GLA, Mercedes-Benz S-Class, and Mercedes-Benz SL
* Why Do Cars Have High Emissions?
    * Manufacturing materials: Steel, aluminum, synthetic plastics, lithium-ion batteries.
    * Complex production processes: Luxury vehicles require more energy-intensive manufacturing.
    * Lithium-ion batteries in electric vehicles (EVs): While EVs reduce operational emissions, their production has a high carbon footprint.
* Luxury cars & SUVs have higher emissions due to their size, manufacturing complexity, and materials.


##### One of the leading industries (7th place) is "Pharmaceuticals, Biotechnology & Life Sciences".
* Data shows that the pharmaceutical and biotechnology industry has significant carbon emissions.
*  Why Does the Pharmaceutical Industry Have High Emissions?
    * Pharmaceutical & biotech manufacturing consumes large amounts of energy.
    * Laboratories use high-power equipment & cooling systems.
    * The global pharmaceutical supply chain increases emissions from transportation.
